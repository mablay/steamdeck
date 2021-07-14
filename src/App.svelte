<script>
  import { getNode, keyTree } from './js/keymap'
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

  function tag (event) {
    const { path } = event.detail
    const record = {
      ...getNode(path),
      time: Date.now()
    }
    history = [record, ...history]
    console.log('TAG |', path.join('/'))
  }

</script>

<main>
  <Hero title="Steamdeck" />
  <Simulator />
  <Breadcrumbs path={path} />

  <div class="row">
    <div class="col-2">
      <Steamdeck bind:path={path} on:tag={tag} />
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