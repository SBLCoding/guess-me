<script>
    let emojiGuess = ["🤔", "😀", "💥", "🦍", "🍉", "🍍", "🥑", "🏆", "🏀", "🎮", "💣", "💈", "🪀", "📻", "🇨🇴", "❤️", "😂", "📢", "🔥", "🐘"]
    let randomEmoji = "🤔"

    $: setInterval(() => {
        randomEmoji = emojiGuess[Math.floor(Math.random() * emojiGuess.length)];
    }, 3000)
</script>

<div class="col-md-12">
    <div class="text-center mt-4">
        <h1 class="guess-me">GUESS {randomEmoji} ME <small class="fs-6">ALPHA</small></h1>
    </div>
</div>

<style>
    .guess-me{
        /*
            font-family: 'Monoton', cursive;
            font-family: 'Press Start 2P', cursive;
            font-family: 'Frijole', cursive;
            font-family: 'Bungee Shade', cursive;
        */

        font-family: 'Bungee Shade', cursive;
        font-size: 80px;
        color: white;
        user-select: none;
    }

    @media (max-width: 800px) {
        .guess-me {
            font-size: 70px;
        }
    }

    @media (max-width: 600px) {
        .guess-me {
            font-size: 60px;
        }
    }

    @media (max-width: 420px) {
        .guess-me {
            font-size: 50px;
        }
    }

    @media (max-width: 380px) {
        .guess-me {
            font-size: 42px;
        }
    }
</style>