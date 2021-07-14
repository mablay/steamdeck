<script>
  export let history
</script>

<div class="history">
  {#each history as record}
  <div class="record">
    {record.time} | {record.icon} | {record.title}
  </div>
  {/each}
</div>

<style>

</style>