<script>
    export let level = 1;
</script>

<div class="profileContainer">
    <img src="https://avatars.githubusercontent.com/u/12385697?s=460&u=ef1337216ad86864942d53c2e72fa069c4b16183&v=4" alt="Ramon Silva" />
    <div>
        <strong>Ramon Silva</strong>
        <p>
            <img src="icons/level.svg" alt="Level" />
            Level {level}
        </p>
    </div>
</div>

<style>
    
    .profileContainer {
        display: flex;
        align-items: center;
    }

    .profileContainer > img {
        width: 5.5rem;
        height: 5.5rem;
        border-radius: 50%;
    }

    .profileContainer div {
        margin-left: 1.5rem;
    }

    .profileContainer div strong {
        font-size: 1.5rem;
        font-weight: 600;
        color: var(--title);
    }

    .profileContainer div p {
        font-size: 1rem;
        margin-top: 0.5rem;
    }

    .profileContainer div p img {
        margin-right: 0.5rem;
    }
</style>
