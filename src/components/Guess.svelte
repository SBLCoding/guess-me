<script>
    import { movies } from '../movies'
    import Attempts from './Attempts.svelte'
	import Correct from './Correct.svelte'
    import Modal from './Modal.svelte'

    /**
     * @TODO Usar el local storage para el puntaje y los intentos
     * @TODO Poder configurar el juego (sonido, colores, peliculas, géneros etc.)
     * @TODO Agregar sonido a las correctas e incorrectas
     */

    let randomMovie = movies[Math.floor(Math.random() * movies.length)];

    let userAttempts = 4
    let userCorrect = 0
    let userGuess = ""
    
    //Modal status
    let isOpen = false
    let modalEmojiContent = '🤔'
    let modalMsgContent = 'GUESS APP'

    //Buscar la siguiente película para adivinar
    const reloadGuess = () => {
        randomMovie = movies[Math.floor(Math.random() * movies.length)]

        if (randomMovie.status === 'displayed') {
            randomMovie = movies[Math.floor(Math.random() * movies.length)]
        }
    }

    //Actualizar status de la película actual, ya no se mostraría
    const updateGuessStatus = () => {
        let movie = movies.find((m) => m.id === randomMovie.id)
        movie.status = 'displayed'
    }

    // on submit
    const guessMe = () => {
        let userGuessLower = userGuess.toLocaleLowerCase()
        let titleMovieLower = randomMovie.title.toLocaleLowerCase()

        validateGuess(userGuessLower, titleMovieLower)
    }

    //Validar si el nombre ingresado e igual a la película para adivinar
    const validateGuess = (guess, movie) => {
        if (guess === movie) {
            userCorrect += 1
            cleanField()
            console.log('😀')
        }else {
            userAttempts -= 1
            cleanField()
            console.log('😞')
        }

        updateGuessStatus()
        reloadGuess()
    }

    //Reiniciar todo si se adivina o queda sin intentos
    const restartGuess = () => {
        userAttempts = 4
        userCorrect = 0
        userGuess = ""

        //Cambiar estado de películas mostradas
        movies.find((movie, index) => {
            if(movie.status === 'displayed')
                movie.status = 'wait'
        })

        //Buscar nuevamente película para mostrar
        randomMovie = movies[Math.floor(Math.random() * movies.length)]

        setTimeout(() => {
            isOpen = false
        }, 5000)
    }

    const cleanField = () => {
        userGuess = ""
    }

    //Validaciones dinámicas
    $: if(userCorrect === 6) {
        isOpen = true
        modalEmojiContent = '🎉'
        modalMsgContent = '¡ERES EXPERT@ EN PELÍCULAS!'

        setTimeout(() => {
            restartGuess()
        }, 1000)
    }

    $: if(userAttempts === 0) {
        isOpen = true
        modalEmojiContent = '😥'
        modalMsgContent = 'SIGUE INTENTANDO'

        setTimeout(() => {
            restartGuess()
        }, 1000)
    }
</script>

<div class="col-md-12 text-center | guessEmoji">
    <h1>{randomMovie.emoji}</h1>
</div>

<form on:submit|preventDefault={guessMe}>
    <div class="col-md-12 mt-4">
        <div class="form-group" style="position: relative;">
            <input 
                class="form-control form-control-lg | guessField" 
                type="text" 
                placeholder="ADIVINA"
                bind:value={userGuess}
            >
            <button type="submit" class="btn btn-secondary | guessButton">OK</button>
        </div>
    </div>
</form>

<div class="col-md-2 col-sm-6">
    <Correct {userCorrect} />
</div>

<div class="col-md-2 col-sm-6 offset-md-8">
    <Attempts {userAttempts} />
</div>

<Modal {isOpen} wraperColor={'transparent'}>
    <div slot="content">
        <div class="text-center user-select-none" style="width: 50vw; margin-bottom: 2.5rem;">
            <h1 class="mb-2 m-4 animate__animated animate__pulse animate__slow animate__infinite modalEmoji">
                {modalEmojiContent}
            </h1>
            <p class="fs-3 mt-4 modalMsg">
                {modalMsgContent}
            </p>
        </div>
    </div>
</Modal>

<style>
    .guessEmoji{
        margin-top: 6rem;
        user-select: none;
    }

    .guessField{
        text-align: center;
        text-transform: uppercase;

        border-radius: 1rem;
        padding-top: 1rem;
        padding-bottom: 1rem;

        font-family: 'Press Start 2P', cursive;
        box-sizing: border-box;
    }

    .guessButton {
        position: absolute;
        right: 3px; 
        top: 3px;
        bottom: 3px;
        line-height: 1 !important;
        z-index: 4;

        padding: 1.2rem;
        border-radius: 1rem;

        background-color: #0096c7;
        border-color: #0096c7;

        font-family: 'Press Start 2P', cursive;

        transition: all ease 300ms;
    }

    .guessButton:hover {
        background-color: #023e8a;
        border-color: #023e8a;
    }

    .guessButton:focus {
        background-color: #023e8a;
        border-color: #023e8a;
    }

    .modalEmoji {
        font-size: 6rem;
        text-shadow: 0 0 10px #fff;
    }

    .modalMsg {
        font-family: 'Press Start 2P', cursive;
        color: white;
    }

    /*Medias*/
    @media (max-width: 800px) {
        .guessField {
            padding-top: 0.6rem;
            padding-bottom: 0.6rem;
        }

        .guessButton {
            padding: 1rem;
        }

        .modalMsg {
            font-size: 1.50rem !important;
        }
    }

    @media (max-width: 600px) {
        .guessField {
            padding-top: 0.4rem;
            padding-bottom: 0.4rem;
            font-size: 1rem;
        }

        .guessButton {
            padding: .7rem;
            font-size: .8rem;
        }

        .guessEmoji{
            margin-top: 5rem;
        }

        .modalMsg {
            font-size: 1.10rem !important;
        }
    }

    @media (max-width: 420px) {
        .guessEmoji{
            margin-top: 4rem;
        }

        .guessField {
            padding-top: 0.2rem;
            padding-bottom: 0.2rem;
        }

        .modalMsg {
            font-size: 1rem !important;
        }
    }

    @media (max-width: 380px) {
        .guessEmoji{
            margin-top: 4rem;
        }

        .guessField {
            padding-top: 0.2rem;
            padding-bottom: 0.2rem;
            font-size: 0.7rem;
        }

        .guessButton {
            padding: .5rem;
            font-size: .7rem;
        }
    }
</style>