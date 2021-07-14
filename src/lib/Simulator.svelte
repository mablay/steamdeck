<script>
	import { onMount } from 'svelte'
  import { keymap } from '../js/keymap'
  const characters = keymap.map(k => k.icon)

  function rndEvent (right) {
    const i = Math.floor(Math.random() * characters.length)
    return {
				character: characters[i],
				x: right ? 100 : Math.random() * 100,
				y: 0 + Math.random() * 20,
				r: 0.2 + Math.random() * 0.8
			}
  }

	let confetti = new Array(2).fill()
		.map((_, i) => rndEvent())
		.sort((a, b) => a.r - b.r);

	onMount(() => {
		let frame;

		function loop() {
			frame = requestAnimationFrame(loop);

			confetti = confetti.map(emoji => {
				emoji.x -= 0.7 * emoji.r;
				if (emoji.x < 0) {
          Object.assign(emoji, rndEvent(true))
        }
				return emoji;
			});
		}

		loop();

		return () => cancelAnimationFrame(frame);
	});
</script>

<div class="simulator">
  {#each confetti as c}
    <span style="left: {c.x}%; top: {c.y}%; transform: scale({c.r})">{c.character}</span>
  {/each}
</div>

<style>
  .simulator {
    width: 100%;
    height: 40px;
  }
	span {
		position: absolute;
		font-size: 5vw;
	}
</style>