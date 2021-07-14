<script>
  import { keyTree } from '../js/keymap'
  export let path
  let breadcrumbs
  // $: breadcrumbs = path.map(n => n.title).join('/')
  $: breadcrumbs = path.join('/')
</script>

<h3 class="text-left">/{breadcrumbs}</h3>

<style>
h3 { text-align: left; }
</style>