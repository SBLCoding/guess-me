<script>
    export let isOpen = false
    export let wraperColor = 'white'

    const open = () => {
        isOpen = true
    }

    const close = () => {
        isOpen = false
    }
</script>

<!--<slot name="trigger" {open}>
    <button on:click={open}>Open modal sape</button>
</slot>-->

{#if isOpen}
    <div class="modal">
        <div class="backdrop" on:click={close} />
        <div class="content-wraper" style="background-color: {wraperColor};">
            <!-- Header -->
            <slot name="header">
                <div class="text-end fs-6 mb-2">
                    <button type="button" class="btn-close" on:click={close}></button>
                </div>
            </slot>

            <!-- Content -->
            <div class="content">
                <slot name="content" />
            </div>

            <!-- Footer -->
            <slot name="footer">
                
            </slot>
        </div>
    </div>
{/if}

<style>
    div.modal {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100vh;

        display: flex;
        justify-content: center;
        align-items: center;
    }

    div.backdrop {
        position: absolute;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.4);
    }

    div.content-wraper {
        z-index: 10;
        max-width: 70vw;
        padding: 1rem;
        border-radius: 1rem;
        overflow: hidden;
    }

    div.content {
        max-height: 50vh;
        overflow: auto;
    }

    .btn-close {
        color: white !important;
    }
</style>