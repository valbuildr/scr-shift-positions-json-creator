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
  <Drivers bind:positions={driverPositions} />
  <Dispatchers bind:positions={dispatcherPositions} />
  <Guards bind:positions={guardPositions} />
  <Signallers bind:positions={signallerPositions} />
  <Supervisors bind:positions={supervisorPositions} />
  <Export
    qdPos={driverPositions}
    dsPos={dispatcherPositions}
    gdPos={guardPositions}
    sgPos={signallerPositions}
    svPos={supervisorPositions}
  />

  <div
    class="bg-slate-700 max-w-screen-xl mx-auto rounded-tl-none rounded-xl p-4 text-white mb-4 dark"
  >
    <p>
      Made with ❤️ by <a href="https://valbuilds.xyz/" class="hover:underline"
        >Valentine</a
      > 🏳️‍⚧️
    </p>
    <p>
      This project has no affiliation with Stepford County Railway or it's
      staff. Please direct any inquires related to SCR to the SCR staff.
    </p>
    <p>
      This project is open source! View the source code <a
        href="https://github.com/valbuildr/scr-shift-positions-json-creator"
        class="hover:underline">here</a
      >.
    </p>
  </div>
</div>
