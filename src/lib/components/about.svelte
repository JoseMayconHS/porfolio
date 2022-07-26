<script>
  export let name = ''
  export let intro = ''
  export let url = ''
</script>

<div class="flex mb-40 items-center flex-col-reverse sm:flex-row">
  <div class="mr-6">
    <h2 class="text-3xl mb-4 font-bold tracking-wider">{name}</h2>
    <p class="text-xl mb-4">{intro}</p>
  </div>

  <img class="mask mask-squircle h-72 sm:h-55" src={url} alt={name} />
</div>
