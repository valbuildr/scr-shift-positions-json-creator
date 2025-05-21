<script lang="ts">
  import { routes, stations } from "$lib";

  import { Button } from "flowbite-svelte";
  import { PlusOutline, TrashBinOutline } from "flowbite-svelte-icons";

  let driverPositions: {
    id: string;
    route?: string;
    depotSpawn?: string;
    note?: string;
    spawnTime: string;
  }[] = $state([]);

  let showNewDriverPositionModal: boolean = $state(false);

  const clearDriverPositions = () => {
    driverPositions = [];
  };

  let dispatcherPositions: {
    id: number;
    station: string;
    platGroup: (string | number)[];
    note?: string;
    spawnTime: string;
  }[] = $state([]);

  let showNewDispatcherPositionModal: boolean = $state(false);

  const clearDispatcherPositions = () => {
    dispatcherPositions = [];
  };

  let guardPositions: {
    id: number;
    train?: string;
    player?: string;
    note?: string;
    spawnTime: string;
  }[] = $state([]);

  let showNewGuardPositionModal: boolean = $state(false);

  const clearGuardPositions = () => {
    guardPositions = [];
  };

  let signallerPositions: {
    id: number;
    zone?: string;
    note?: string;
    spawnTime: string;
  }[] = $state([]);

  let showNewSignallerPositionModal: boolean = $state(false);

  const clearSignallerPositions = () => {
    signallerPositions = [];
  };

  let supervisorPositions: {
    id: number;
    note?: string;
    spawnTime: string;
  }[] = $state([]);

  let showNewSupervisorPositionModal: boolean = $state(false);

  const clearSupervisorPositions = () => {
    supervisorPositions = [];
  };
</script>

<div class="min-h-screen bg-slate-800 pt-4 dark">
  <div
    class="bg-slate-700 max-w-screen-xl mx-auto rounded-tl-none rounded-xl p-4 text-white"
  >
    {#if driverPositions.length == 0 && dispatcherPositions.length == 0 && guardPositions.length == 0 && signallerPositions.length == 0 && supervisorPositions.length == 0}
      <div
        class="bg-red-900 border border-red-500 rounded-xl rounded-tl-none mb-2 p-2"
      >
        <p>No positions added. You must add at least one.</p>
      </div>
    {/if}

    {#if supervisorPositions.length == 0}
      <div
        class="bg-red-900 border border-red-500 rounded-xl rounded-tl-none mb-2 p-2"
      >
        <p>
          No supervisor positions added. You must add at least one, make sure to
          add yourself!
        </p>
      </div>
    {/if}

    <div class="flex gap-2 items-center">
      <p class="text-2xl p-1.5 bg-qd w-fit rounded-xl font-medium">QD</p>
      <p class="text-2xl">Qualified Driver Positions</p>
      <Button
        size="sm"
        color="light"
        onclick={() => {
          showNewDriverPositionModal = true;
        }}><PlusOutline class="me-2 h-4 w-4" />Add</Button
      >
      <Button
        size="sm"
        color="light"
        onclick={clearDriverPositions}
        disabled={driverPositions.length == 0}
        ><TrashBinOutline class="me-2 h-4 w-4" />Clear</Button
      >
    </div>

    {#if driverPositions.length == 0}
      <div
        class="bg-slate-600 border border-slate-500 text-slate-400 rounded-xl rounded-tl-none mt-2 p-2"
      >
        <p>No qualified driver positions added.</p>
      </div>
    {/if}

    <hr class="my-2 border-slate-500" />

    <div class="flex gap-2 items-center">
      <p class="text-2xl p-1.5 bg-ds w-fit rounded-xl font-medium">DS</p>
      <p class="text-2xl">Dispatcher Positions</p>
      <Button size="sm" color="light"
        ><PlusOutline class="me-2 h-4 w-4" />Add</Button
      >
      <Button
        size="sm"
        color="light"
        onclick={clearDispatcherPositions}
        disabled={dispatcherPositions.length == 0}
        ><TrashBinOutline class="me-2 h-4 w-4" />Clear</Button
      >
    </div>

    {#if dispatcherPositions.length == 0}
      <div
        class="bg-slate-600 border border-slate-500 text-slate-400 rounded-xl rounded-tl-none mt-2 p-2"
      >
        <p>No dispatcher positions added.</p>
      </div>
    {/if}

    <hr class="my-2 border-slate-500" />

    <div class="flex gap-2 items-center">
      <p class="text-2xl p-1.5 bg-gd w-fit rounded-xl font-medium">GD</p>
      <p class="text-2xl">Guard Positions</p>
      <Button size="sm" color="light"
        ><PlusOutline class="me-2 h-4 w-4" />Add</Button
      >
      <Button
        size="sm"
        color="light"
        onclick={clearGuardPositions}
        disabled={guardPositions.length == 0}
        ><TrashBinOutline class="me-2 h-4 w-4" />Clear</Button
      >
    </div>

    {#if guardPositions.length == 0}
      <div
        class="bg-slate-600 border border-slate-500 text-slate-400 rounded-xl rounded-tl-none mt-2 p-2"
      >
        <p>No guard positions added.</p>
      </div>
    {/if}

    <hr class="my-2 border-slate-500" />

    <div class="flex gap-2 items-center">
      <p class="text-2xl p-1.5 bg-sg w-fit rounded-xl font-medium">SQ</p>
      <p class="text-2xl">Signaller Positions</p>
      <Button size="sm" color="light"
        ><PlusOutline class="me-2 h-4 w-4" />Add</Button
      >
      <Button
        size="sm"
        color="light"
        onclick={clearSignallerPositions}
        disabled={signallerPositions.length == 0}
        ><TrashBinOutline class="me-2 h-4 w-4" />Clear</Button
      >
    </div>

    {#if signallerPositions.length == 0}
      <div
        class="bg-slate-600 border border-slate-500 text-slate-400 rounded-xl rounded-tl-none mt-2 p-2"
      >
        <p>No signaller positions added.</p>
      </div>
    {/if}

    <hr class="my-2 border-slate-500" />

    <div class="flex gap-2 items-center">
      <p class="text-2xl p-1.5 bg-sv w-fit rounded-xl font-medium">SV</p>
      <p class="text-2xl">Supervisior Positions</p>
      <Button size="sm" color="light"
        ><PlusOutline class="me-2 h-4 w-4" />Add</Button
      >
      <Button
        size="sm"
        color="light"
        onclick={clearSupervisorPositions}
        disabled={supervisorPositions.length == 0}
        ><TrashBinOutline class="me-2 h-4 w-4" />Clear</Button
      >
    </div>

    {#if supervisorPositions.length == 0}
      <div
        class="bg-slate-600 border border-slate-500 text-slate-400 rounded-xl rounded-tl-none mt-2 p-2"
      >
        <p>
          No supervisor positions added. <b
            >You must have at least one, make sure to add yourself!</b
          >
        </p>
      </div>
    {/if}

    <hr class="my-2 border-slate-500" />

    <div class="flex gap-2 items-center">
      <Button color="light"><PlusOutline class="me-2 h-5 w-5" />Export</Button>
    </div>
  </div>
</div>
