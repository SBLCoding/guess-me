<script>
    export let userCorrect = 0
</script>

<div class="text-center mt-5 userCorrect">
    <h2>{userCorrect}</h2>
    <p>CORRECTAS</p>
</div>

<style>
    .userCorrect {
        font-family: 'Press Start 2P', cursive;
        color: white;
        position: relative;
        z-index: 4;
    }

    .userCorrect > p {
        font-size: 8px;
    }
</style>