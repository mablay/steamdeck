<script>
  import Button from './Button.svelte'
  import { keyTree } from './keymap'
  import Simulator from './Simulator.svelte'
  let node = keyTree
  let keys = Object.keys(node.keys)
  let path = []
  let history = []
  
  document.onkeydown = e => select(e)

  function select (event) {
    const key = event.key
    if (key === 'Escape') {
      up()
      return
    }
    if (!~keys.indexOf(key)) return
    console.log('select', key)
    const value = node.keys[key]
    if (!value.keys) {
      history = [...history, {
        time: Date.now(),
        ...value
      }]
      node = keyTree
      keys = Object.keys(node.keys)
      path = []
      return
    }
    node = node.keys[key]
    keys = Object.keys(node.keys)
    path = [...path, {
      key,
      title: node.title,
      icon: node.icon
    }]
    console.log(path)

    // path.push(key)
  }

  // move one level backwards in the path
  function up () {
    node = keyTree
    path.pop()
    for (const seg of path.map(n => n.key)) {
      node = node.keys[seg]
    }
    path = path // svelte needs that to update the UI
    keys = Object.keys(node.keys)
    console.log(keys)
  }
</script>

<main>
  <div class="hero">
    <h1>SteamDeck</h1>
  </div>
  <Simulator />
  <h3 class="text-left">/{ path.map(n => n.title).join('/') }</h3>
  <div class="row">
    <div class="column">
      {#each keys as key}
      <div class="text-left">
        {key} | { node.keys[key].icon } | { node.keys[key].title }
      </div>
      {/each}
    </div>
    <div class="column">
      <pre class="text-left">
        {#each history as record}{record.time} | {record.icon} | {record.title}{@html '\n'}{/each}
      </pre>
    </div>
  </div>


  <!-- <Button ></Button> -->
</main>

<style>
  /* :global(body) {
    background-color: grey;
  } */

	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

  .hero {
    height: 130px;
    width: 100%;
  }

	h1 {
    position: absolute;
    top: 60px;
    margin: auto;
    width: 100%;
    text-align: center;
    z-index: 100;
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
    text-shadow: 0 0 10px #fff;
	}

  .text-left {
    text-align: left;
  }

  .column {
    float: left;
    width: 50%;
  }

  /* Clear floats after the columns */
  .row:after {
    content: "";
    display: table;
    clear: both;
  }

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>