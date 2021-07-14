<script>
  import { keyTree } from './js/keymap'
  import Simulator from './lib/Simulator.svelte'
  import Footer from './lib/Footer.svelte'
  import Breadcrumbs from './lib/Breadcrumbs.svelte'
  import Steamdeck from './lib/Steamdeck.svelte'
  import History from './lib/History.svelte'
  import Hero from './lib/Hero.svelte'

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
  <Hero title="Steamdeck" />
  <Simulator />
  <Breadcrumbs path={path} />

  <div class="row">
    <div class="col-2">
      {#each keys as key}
      <div class="text-left">
        {key} | { node.keys[key].icon } | { node.keys[key].title }
      </div>
      {/each}
      <Steamdeck bind:path={path} />
    </div>
    <div class="col-2">
      <pre class="text-left">
        <History history={history} />
      </pre>
    </div>
  </div>


  <Footer/>
</main>

<style>
	main {
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>