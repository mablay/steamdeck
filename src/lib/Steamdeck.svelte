<script>
  import { onMount } from 'svelte'
  import { keyTree } from '../js/keymap'
  import Keyboard from './Keyboard.svelte'
  export let path
  let self

  // document.onkeydown = e => select(e)
  function up () {
    console.log('up')
    if (path.length === 0) return
    path.pop()
    path = path
  }

  function down (event) {
    const key = String.fromCharCode(97 + event.clientX % 26)
    console.log('down', key)
    path = [...path, key]
  }

  function keydown (event) {
    console.log(event)
  }

  function focus (event) {
    if (event) {
      console.log('blur => refocus')
    } else {
      console.log('focus')
    }
    this.focus()
  }

  function focussed () {
    console.log('focussed')
  }

  onMount(() => self.focus())
</script>

<div id="steamdeck" tabindex="0" bind:this="{self}" on:blur="{focus}" on:focus={focussed} on:keydown={keydown}>
  <div class="when-inactive">
    <p>Click to activate</p>
    <p>STEAMDECK</p>
  </div>
  <div class="when-active">
    <Keyboard />
  </div>
</div>

<style>
#steamdeck {
  position: relative;
  width: 400px;
  height: 400px;
  border-radius: 10px;
  background-color: grey;
  box-shadow: inset 0 0 10px #444;
  transition: background-color 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
}

#steamdeck:focus {
  outline: none;
  background-color: white;
  box-shadow: 0 0 10px #AAA;
  transition: box-shadow 0.3s ease-in-out, background-color 0.3s ease-in-out;
}

.when-inactive {
  position: absolute;
  width: 400px;
  height: 400px;
  color: white;
  font-family: "HelveticaNeue-Light", "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial, "Lucida Grande", sans-serif;   
  font-size: 24px;
  padding: 120px 20px 20px ;
  text-align: center;
  vertical-align: middle;
}

.when-active {
  position: absolute;
  width: 400px;
  height: 400px;
  color: black;
  background-color: transparent;
  padding: 20px;
}

@keyframes fadein {
    from { opacity: 0; }
    to   { opacity: 1; }
}

button {
  animation: fadein 1s;
}


#steamdeck > .when-inactive { display: block }
#steamdeck:focus > .when-inactive { display: none }

#steamdeck > .when-active { display: none }
#steamdeck:focus > .when-active { display: block }

</style>