<script>
    export let percentToNextLevel = 0;
    export let currentExperience = 0;
    export let experienceToNextLevel = 0;
</script>

<header class="experienceBar">
    <span>0 xp</span>
    <div>
        <div style="width: {percentToNextLevel}%" />
        <span class="currentExperience" style="left: {percentToNextLevel}%">
            {currentExperience}xp
        </span>
    </div>
    <span>{experienceToNextLevel} xp</span>
</header>

<style>
    .experienceBar {
        display: flex;
        align-items: center;
    }

    .experienceBar span {
        font-size: 1rem;
    }

    .experienceBar > div {
        flex: 1;
        height: 4px;
        border-radius: 4px;
        background: var(--gray-line);
        margin: 0 1.5rem;
        position: relative;
    }

    .experienceBar > div > div {
        height: 4px;
        border-radius: 4px;
        background: var(--green);
    }

    span.currentExperience {
        position: absolute;
        top: 12px;
        transform: translateX(-50%);
    }
</style>
