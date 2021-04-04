<script>
    export let userAttempts = 4
</script>

<div class="text-center mt-5 userAttempts">
    <h2>{userAttempts}</h2>
    <p>INTENTOS</p>
</div>

<style>
    .userAttempts {
        font-family: 'Press Start 2P', cursive;
        color: white;
        position: relative;
        z-index: 4;
    }

    .userAttempts > p {
        font-size: 8px;
    }
</style>