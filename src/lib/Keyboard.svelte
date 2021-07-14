<script>
  import { keyTree } from '../js/keymap'
  export let path
  let keyboard = {
    q: 'Q', w: 'W', e: 'E',
    a: 'A', s: 'S', d: 'D',
    y: 'Y', x: 'X', c: 'C'
  }
</script>

<div class="keyboard">
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