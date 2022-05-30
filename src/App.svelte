<script>
	let timeLeftMin = 0;
	let timeLeftSec = 0;
	let time = "00:00";
	let shotClock = 24;
	let period = 1;
	let pause = true;
	let selected;

	class team {
		constructor(name) {
			this.name = name;
			this.score = 0;
			this.fouls = 0;
		}
	}

	var team1 = new team("LIGHT");
	var team2 = new team("DARK");

	function updateTime() {
		time =
			("0" + timeLeftMin).slice(-2) + ":" + ("0" + timeLeftSec).slice(-2);
	}

	function handleKeydown(event) {
		let key = event.key;
		if (key === " ") {
			if (time === "00:00") {
				timeLeftMin = 20;
				time = "20:00";
			}
			if (pause) {
				pause = false;
			} else {
				pause = true;
			}
			if (shotClock === 0) {
				shotClock = 24;
			}
		}

		if (key === "Enter") {
			shotClock = 24;
		}

		if (key === "p") {
			if (period < 4) {
				period += 1;
			}
		}

		if (key === "P") {
			if (period > 1) {
				period -= 1;
			}
		}

		if (key === "1") {
			if (selected === "light") {
				team1.score += 1;
			}
			if (selected === "dark") {
				team2.score += 1;
			}
		}

		if (key === "!") {
			if (selected === "light") {
				team1.score -= 1;
			}
			if (selected === "dark") {
				team2.score -= 1;
			}
		}
		if (key === "2") {
			if (selected === "light") {
				team1.score += 2;
			}
			if (selected === "dark") {
				team2.score += 2;
			}
		}

		if (key === "@") {
			if (selected === "light") {
				team1.score -= 2;
			}
			if (selected === "dark") {
				team2.score -= 2;
			}
		}
		if (key === "3") {
			if (selected === "light") {
				team1.score += 3;
			}
			if (selected === "dark") {
				team2.score += 3;
			}
		}

		if (key === "#") {
			if (selected === "light") {
				team1.score -= 3;
			}
			if (selected === "dark") {
				team2.score -= 3;
			}
		}

		if (key === "f") {
			if (selected === "light") {
				team1.fouls += 1;
			}
			if (selected === "dark") {
				team2.fouls += 1;
			}
		}
		if (key === "F") {
			if (selected === "light") {
				team1.fouls -= 1;
			}
			if (selected === "dark") {
				team2.fouls -= 1;
			}
		}
	}

	function lightClick() {
		selected = "light";
	}
	function darkClick() {
		selected = "dark";
	}

	updateTime();
	setInterval(function () {
		if (!pause) {
			if (time === "00:00") {
				shotClock = 24;
			} else {
				if (shotClock > 0) {
					shotClock -= 1;
				} else {
					pause = true;
				}
				if (timeLeftSec > 0) {
					timeLeftSec -= 1;
					updateTime();
				} else {
					if (timeLeftMin > 0) {
						timeLeftMin -= 1;
						timeLeftSec = 59;
						updateTime();
					}
				}
			}
		}
	}, 1000);
</script>

<svelte:window on:keydown={handleKeydown} />

<main>
	<body>
		<div id="time">{time}</div>

		<div class="row">
			<div id="team1" class="column team1" on:click={lightClick}>
				<div id="score">
					<p>{team1.name}</p>
					{team1.score}
				</div>
				<div id="fouls">
					<p>FOULS</p>
					{team1.fouls}
				</div>
			</div>

			<div class="column middle">
				<div id="period">
					<p>PERIOD</p>
					{period}
				</div>
				<div id="shotClock">{shotClock}</div>
			</div>

			<div id="team2" class="column team2" on:click={darkClick}>
				<div id="score">
					<p>{team2.name}</p>
					{team2.score}
				</div>
				<div id="fouls">
					<p>FOULS</p>
					{team2.fouls}
				</div>
			</div>
		</div>
	</body>
</main>

<style>
	body {
		text-align: center;
	}
	p {
		font-size: 4vh;
		margin: 0px;
	}

	#time {
		height: 30vh;

		font-size: 25vh;
	}

	.column {
		float: left;
		height: 70vh;
	}

	.team1,
	.team2 {
		width: 30%;
	}

	.middle {
		width: 40%;
	}

	#score {
		height: 60%;

		font-size: 25vmin;
	}
	#fouls {
		height: 40%;
		font-size: 15vmin;
	}

	#period {
		height: 22%;

		margin-top: 3%;

		font-size: 10vmin;
	}
	#shotClock {
		height: 75%;

		font-size: 40vmin;
	}
</style>
