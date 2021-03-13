<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    export let amount = 0;
    export let type;
    export let description;

    function handleChallengeFailed() {
        dispatch('failed');
    }

    function handleChallengeSucceeded() {
        dispatch('succeeded');
    }
</script>

<div class="challengeBoxContainer">
    {#if amount}
        <div class="challengeActive">
            <header>Ganhe {amount} xp</header>

            <main>
                <img src="icons/{type}.svg" alt="" />
                <strong>Novo desafio</strong>
                <p>{description}</p>
            </main>

            <footer>
                <button
                    type="button"
                    class="challengeFailedButton"
                    on:click={handleChallengeFailed}>Falhei</button
                >
                <button
                    type="button"
                    class="challengeSucceededButton"
                    on:click={handleChallengeSucceeded}>Completei</button
                >
            </footer>
        </div>
    {:else}
        <div class="challengeNotActive">
            <strong>Finalize um ciclo para receber um desafio! </strong>
            <p>
                <img src="icons/level-up.svg" alt="Level Up" />
                Avance de level completando desafios.
            </p>
        </div>
    {/if}
</div>

<style>
    .challengeBoxContainer {
        height: 100%;
        background: var(--white);
        border-radius: 5px;
        box-shadow: 0 0 60px rgba(0, 0, 0, 0.05);
        padding: 1.5rem 2rem;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        text-align: center;
    }

    .challengeNotActive {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .challengeNotActive strong {
        font-size: 1.5rem;
        font-weight: 500;
        line-height: 1.4;
    }

    .challengeNotActive p {
        display: flex;
        flex-direction: column;
        align-items: center;
        line-height: 1.4;
        max-width: 70%;
        margin-top: 3rem;
    }

    .challengeNotActive p img {
        margin-bottom: 1rem;
    }

    .challengeActive {
        height: 100%;
        display: flex;
        flex-direction: column;
    }

    .challengeActive header {
        color: var(--blue);
        font-weight: 600;
        font-size: 1.25rem;
        padding: 0 2rem 1.5rem;
        border-bottom: 1px solid var(--gray-line);
    }

    .challengeActive main {
        flex: 1;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    .challengeActive main strong {
        font-size: 2rem;
        font-weight: 600;
        color: var(--title);
        margin: 1.5rem 0 1rem;
    }

    .challengeActive main p {
        line-height: 1.5;
    }

    .challengeActive footer {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 1rem;
    }

    .challengeActive footer button {
        height: 3rem;
        display: flex;
        align-items: center;
        justify-content: center;
        border: 0;
        border-radius: 5px;
        color: var(--white);
        font-size: 1rem;
        font-weight: 600;
        transition: filter 0.2s;
    }

    .challengeActive footer button.challengeFailedButton {
        background: var(--red);
    }

    .challengeActive footer button.challengeSucceededButton {
        background: var(--green);
    }

    .challengeActive footer button:hover {
        filter: brightness(0.9);
    }
</style>
