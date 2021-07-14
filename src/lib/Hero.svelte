<script>
  export let title
</script>

<div class="hero">
  <h1>{title}</h1>
</div>

<style>
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
</style>