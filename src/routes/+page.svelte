<script lang="ts">
  let driverPositions: { id: number; route: string; depotSpawn: string }[] =
    $state([]);
</script>

<div class="min-h-screen bg-slate-800 pt-4">
  <div
    class="bg-slate-700 max-w-screen-xl mx-auto rounded-tl-none rounded-xl p-4 text-white"
  >
    <!-- {#if} -->

    <div class="flex gap-2 items-center">
      <p class="text-2xl p-1.5 bg-qd w-fit rounded-xl font-medium">QD</p>
      <p class="text-2xl">Qualified Driver Positions</p>
    </div>

    <hr class="my-2 border-slate-500" />

    <div class="flex gap-2 items-center">
      <p class="text-2xl p-1.5 bg-ds w-fit rounded-xl font-medium">DS</p>
      <p class="text-2xl">Dispatcher Positions</p>
    </div>

    <hr class="my-2 border-slate-500" />

    <div class="flex gap-2 items-center">
      <p class="text-2xl p-1.5 bg-gd w-fit rounded-xl font-medium">GD</p>
      <p class="text-2xl">Guard Positions</p>
    </div>

    <hr class="my-2 border-slate-500" />

    <div class="flex gap-2 items-center">
      <p class="text-2xl p-1.5 bg-sg w-fit rounded-xl font-medium">SQ</p>
      <p class="text-2xl">Signaller Positions</p>
    </div>

    <hr class="my-2 border-slate-500" />

    <div class="flex gap-2 items-center">
      <p class="text-2xl p-1.5 bg-sv w-fit rounded-xl font-medium">SV</p>
      <p class="text-2xl">Supervisior Positions</p>
    </div>
  </div>
</div>
