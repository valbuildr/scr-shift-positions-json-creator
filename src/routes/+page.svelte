<script lang="ts">
  import Drivers from "$lib/Drivers.svelte";
  import Dispatchers from "$lib/Dispatchers.svelte";
  import Guards from "$lib/Guards.svelte";
  import Signallers from "$lib/Signallers.svelte";
  import Supervisors from "$lib/Supervisors.svelte";
  import Export from "$lib/Export.svelte";

  let driverPositions = $state([]);
  let dispatcherPositions = $state([]);
  let guardPositions = $state([]);
  let signallerPositions = $state([]);
  let supervisorPositions = $state([]);
</script>

<div class="min-h-screen bg-slate-800 py-4 dark">
  {#if (driverPositions.length == 0 && dispatcherPositions.length == 0 && guardPositions.length == 0 && signallerPositions.length == 0 && supervisorPositions.length == 0) || supervisorPositions.length == 0}
    <div
      class="bg-slate-700 max-w-screen-xl mx-auto rounded-tl-none rounded-xl p-4 text-white mb-4"
    >
      {#if driverPositions.length == 0 && dispatcherPositions.length == 0 && guardPositions.length == 0 && signallerPositions.length == 0 && supervisorPositions.length == 0}
        <div
          class="bg-red-900 border border-red-500 rounded-xl rounded-tl-none my-2 p-2"
        >
          <p>No positions added. You must add at least one.</p>
        </div>
      {/if}

      {#if supervisorPositions.length == 0}
        <div
          class="bg-red-900 border border-red-500 rounded-xl rounded-tl-none my-2 p-2"
        >
          <p>
            No supervisor positions added. You must add at least one, make sure
            to add one for yourself!
          </p>
        </div>
      {/if}

      {#if driverPositions.length + dispatcherPositions.length + guardPositions.length + signallerPositions.length + supervisorPositions.length > 75}
        <div
          class="bg-red-900 border border-red-500 rounded-xl rounded-tl-none my-2 p-2"
        >
          <p>
            Too many positions. You currently have {driverPositions.length +
              dispatcherPositions.length +
              guardPositions.length +
              signallerPositions.length +
              supervisorPositions.length} positions. The maximum is 75.
          </p>
        </div>
      {/if}

      {#if driverPositions.length + dispatcherPositions.length + guardPositions.length + signallerPositions.length + supervisorPositions.length == 75}
        <div
          class="bg-yellow-900 border border-yellow-500 rounded-xl rounded-tl-none my-2 p-2"
        >
          <p>
            Maximum number of positions reached. You can only have 75 positions.
          </p>
        </div>
      {/if}
    </div>
  {/if}

  <Drivers bind:positions={driverPositions} />
  <Dispatchers bind:positions={dispatcherPositions} />
  <Guards bind:positions={guardPositions} />
  <Signallers bind:positions={signallerPositions} />
  <Supervisors bind:positions={supervisorPositions} />
  <Export />
</div>
