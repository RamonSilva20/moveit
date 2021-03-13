<script>
	import Countdown from "./components/Countdown.svelte";
	import ExperienceBar from "./components/ExperienceBar.svelte";
	import Profile from "./components/Profile.svelte";
	import CompletedChallenges from "./components/CompletedChallenges.svelte";
	import ChallengeBox from "./components/ChallengeBox.svelte";

	import {
		currentExperience,
		experienceToNextLevel,
		level,
		challengesCompleted,
		activeChallenge,
		challenges,
	} from "./stores/challenges";

	let type,
		description = "";
	let amount = 0;
	let hasFinished;

	$: percentToNextLevel =
		Math.round($currentExperience * 100) / $experienceToNextLevel;

	function finishedCountdown(event) {
		hasFinished = event.detail;
		startNewChallenge();
	}

	function chalengeFailed() {
		amount = 0;
		hasFinished = false;
	}

	function chalangeSucceeded() {
		amount = 0;
		hasFinished = false;

		let finalExperience = $activeChallenge + $currentExperience;

		if (finalExperience >= $experienceToNextLevel) {
			finalExperience = finalExperience - $experienceToNextLevel;
			level.set(($level += 1));
		}

		currentExperience.set(finalExperience);
		activeChallenge.set(0);
		challengesCompleted.set($challengesCompleted + 1);
	}

	function startNewChallenge() {
		const randomChallengeIndex = Math.floor(
			Math.random() * $challenges.length
		);
		const challenge = $challenges[randomChallengeIndex];
		activeChallenge.set(challenge.amount);

		type = challenge.type;
		amount = challenge.amount;
		description = challenge.description;

		notify(amount);
	}

	function notify(amount) {

		new Audio("/notification.mp3").play();

		// check if browser has support
		if (!("Notification" in window)) {
			console.log();
		}

		// check if has permission
		else if (Notification.permission === "granted") {
			new Notification("Novo desafio 🎉", {
				body: `valendo ${amount} xp!`,
			});
		}
		// ask user
		else if (Notification.permission !== "denied") {
			Notification.requestPermission().then(function (permission) {
				if (permission === "granted") {
					new Notification("Novo desafio 🎉", {
						body: `valendo ${amount} xp!`,
					});
				}
			});
		}
	}
</script>

<main>
	<div class="container">
		<ExperienceBar
			currentExperience={$currentExperience}
			experienceToNextLevel={$experienceToNextLevel}
			{percentToNextLevel}
		/>
		<section>
			<div>
				<Profile level={$level} />
				<CompletedChallenges
					challengesCompleted={$challengesCompleted}
				/>
				<Countdown on:finished={finishedCountdown} {hasFinished} />
			</div>
			<div>
				<ChallengeBox
					{amount}
					{type}
					{description}
					on:failed={chalengeFailed}
					on:succeeded={chalangeSucceeded}
				/>
			</div>
		</section>
	</div>
</main>

<style>
	.container {
		height: 100vh;
		max-width: 992px;
		margin: 0 auto;
		padding: 2.5rem 2rem;
		display: flex;
		flex-direction: column;
	}

	.container section {
		flex: 1;
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 6.25rem;
		align-content: center;
	}
</style>
