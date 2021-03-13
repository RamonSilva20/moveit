<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();
    export let hasFinished = false;

    let countdown = 25 * 60;
    let isActive, timer;
    let minutes, seconds = 0;
    $: minutes = countdown > 59 ? Math.floor(countdown / 60) : 0;
    $: seconds = countdown % 60;

    $: if (countdown == 0) {
        countdown = 25 * 60;
        hasFinished = true;
        resetCountdown();
        dispatch("finished", hasFinished);
    }

    function resetCountdown() {
        clearInterval(timer);
        countdown = 25 * 60;
        isActive = false;
    }

    function startCountdown() {
        timer = setInterval(() => {
            countdown = countdown - 1;
        }, 1000);
        isActive = true;
    }
</script>

<div>
    <div class="countdownContainer">
        <div>
            <span>{String(minutes).padStart(2, "0")}</span>
        </div>
        <span>:</span>
        <div>
            <span>{String(seconds).padStart(2, "0")}</span>
        </div>
    </div>
    {#if hasFinished}
        <button disabled class="countdownButton"> Ciclo encerrado </button>
    {:else if isActive}
        <button
            type="button"
            class="countdownButton countdownButtonActive"
            on:click={resetCountdown}>Abandonar ciclo</button
        >
    {:else}
        <button type="button" class="countdownButton" on:click={startCountdown}
            >Iniciar ciclo</button
        >
    {/if}
</div>

<style>
    .countdownContainer {
        display: flex;
        align-items: center;
        font-family: Rajdhani;
        font-weight: 600;
        color: var(--title);
    }

    .countdownContainer > div {
        flex: 1;
        display: flex;
        align-items: center;
        justify-content: space-evenly;
        background: var(--white);
        box-shadow: 0 0 60px rgba(0, 0, 0, 0.05);
        border-radius: 5px;
        font-size: 8.5rem;
        text-align: center;
    }

    .countdownContainer > div span {
        flex: 1;
    }

    .countdownContainer > div span:first-child {
        border-right: 1px solid #f0f1f3;
    }

    .countdownContainer > div span:last-child {
        border-left: 1px solid #f0f1f3;
    }

    .countdownContainer > span {
        font-size: 6.25rem;
        margin: 0 0.5rem;
    }

    .countdownButton {
        width: 100%;
        height: 5rem;
        margin-top: 2rem;
        display: flex;
        align-items: center;
        justify-content: center;
        border: 0;
        border-radius: 5px;
        background: var(--blue);
        color: var(--white);
        font-size: 1.25rem;
        font-weight: 600;
        transition: background-color 0.2s;
    }

    .countdownButton:not(:disabled):hover {
        background: var(--blue-dark);
    }

    .countdownButtonActive {
        background: var(--white);
        color: var(--title);
    }

    .countdownButtonActive:not(:disabled):hover {
        background: var(--red);
        color: var(--white);
    }

    .countdownButton:disabled {
        background: var(--white);
        color: var(--text);
        cursor: not-allowed;
    }
</style>
