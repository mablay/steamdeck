<script>
	import { createEventDispatcher } from 'svelte'
  import { getNode } from '../js/keymap'
  export let path
  
  const dispatch = createEventDispatcher()

  $: node = getNode(path)
  let keyboard = {
    q: 'Q', w: 'W', e: 'E',
    a: 'A', s: 'S', d: 'D',
    y: 'Y', x: 'X', c: 'C'
  }

  $: {
    for (const key in keyboard) {
      if (node.keys[key]) {
        keyboard[key] = node.keys[key].icon || '?'
      } else {
        keyboard[key] = key
      }
    }
  }

  export function keydown (event) {
    // console.log('KEYDOWN |', event.key)
    const key = event.key
    if (key === 'Escape') {
      console.log('up()')
      // up()
      return
    }
    const next = node.keys[key]
    if (!next) return
    if (!next.keys) {
      dispatch('tag', { path: [...path, key] })
      path = []
      // console.log('root options', Object.keys(getNode().keys).join(', '))
    } else {
      path = [...path, key]
      // console.log('options', Object.keys(next.keys).join(', '))
    }

  }

</script>

<div class="keyboard">
  {node.icon}
  <div class="key q">{keyboard.q}</div>
  <div class="key w">{keyboard.w}</div>
  <div class="key e">{keyboard.e}</div>
  <div class="key a">{keyboard.a}</div>
  <div class="key s">{keyboard.s}</div>
  <div class="key d">{keyboard.d}</div>
  <div class="key y">{keyboard.y}</div>
  <div class="key x">{keyboard.x}</div>
  <div class="key c">{keyboard.c}</div>
</div>

<style>
.keyboard {
  position: relative;
  height: 400px;
  width: 400px;
}

.key {
  position: absolute;
  width: 80px;
  height: 80px;
  border: 1px solid grey;
  text-align: center;
  line-height: 80px;
}
.q { left: 40px; top: 40px; }
.w { left: 140px; top: 40px; }
.e { left: 240px; top: 40px; }

.a { left: 40px; top: 140px; }
.s { left: 140px; top: 140px; }
.d { left: 240px; top: 140px; }

.y { left: 40px; top: 240px; }
.x { left: 140px; top: 240px; }
.c { left: 240px; top: 240px; }
</style>