<script lang="ts">
  import type { DispatcherPositionInfo } from "$lib";
  import { stations } from "$lib";

  import { Button, Modal, Label, Input, Select } from "flowbite-svelte";

  let { positions = $bindable() }: { positions: DispatcherPositionInfo[] } =
    $props();

  let showModal: boolean = $state(false);
  let newPositionData: DispatcherPositionInfo = $state({ id: "" });

  const pushNewPosition = () => {
    if (newPositionData.id == "") {
      alert("An ID is required.");
    } else {
      positions.push(newPositionData);
      showModal = false;
      clearNewPositionData();
    }
  };
  const clearNewPositionData = () => {
    newPositionData = { id: "" };
  };

  let formattedStations: { value: string; name: string }[] = [];
  for (const station of Object.entries(stations)) {
    formattedStations.push({ value: station[0], name: station[1].name });
  }

  let groups: { value: string; name: string }[] = $state([]);
  const updateGroups = () => {
    groups = [];

    const station =
      stations[newPositionData.station ? newPositionData.station : ""];
    if (station && Array.isArray(station.dsGroups)) {
      for (const group of station.dsGroups) {
        groups.push({ value: group.toString(), name: group.toString() });
      }
    }
  };
</script>

<div
  class="bg-slate-700 max-w-screen-xl mx-auto rounded-tl-none rounded-xl p-4 text-white mb-4 dark"
>
  <div class="flex gap-2 items-center">
    <p class="text-2xl p-1.5 bg-ds w-fit rounded-xl font-medium">DS</p>
    <p class="text-2xl">Dispatcher Positions</p>

    <Button
      size="sm"
      color="light"
      onclick={() => {
        showModal = true;
      }}
    >
      Add
    </Button>
    <Button
      size="sm"
      color="light"
      onclick={() => {
        positions = [];
      }}
      disabled={positions.length == 0}
    >
      Clear
    </Button>
  </div>

  {#if positions.length == 0}
    <div
      class="bg-slate-600 border border-slate-500 text-slate-400 rounded-xl rounded-tl-none mt-2 p-2"
    >
      <p>No dispatcher positions added.</p>
    </div>
  {:else}
    {#each positions as pos}
      <div
        class="bg-slate-600 border border-slate-500 rounded-xl rounded-tl-none mt-2 p-2 grid grid-cols-6 items-center"
      >
        <p>{pos.id}</p>
        <p>{pos.station ? pos.station : "Any station"}</p>
        <p>{pos.platforms ? pos.platforms : "Any platform group"}</p>
        <p>{pos.time ? pos.time : "Any time"}</p>
        <p>{pos.note}</p>
        <Button
          size="xs"
          color="light"
          onclick={() => positions.splice(positions.indexOf(pos), 1)}
        >
          Delete
        </Button>
      </div>
    {/each}
  {/if}

  <Modal title="New Dispatcher Position" bind:open={showModal}>
    <Label for="modal-id" class="ml-1 mb-2">ID</Label>
    <Input
      type="number"
      id="modal-id"
      class="mb-2"
      min="1"
      bind:value={newPositionData.id}
    />

    <Label for="modal-station" class="ml-1 mb-2">Station</Label>
    <Select
      id="modal-station"
      class="mb-2"
      bind:value={newPositionData.station}
      items={formattedStations}
      onchange={updateGroups}
    />

    <Label for="modal-group" class="ml-1 mb-2">Group</Label>
    <Select
      id="modal-group"
      class="mb-2"
      bind:value={newPositionData.platforms}
      items={groups}
      disabled={newPositionData.station == undefined}
    />

    <Label for="modal-note" class="ml-1 mb-2">Note</Label>
    <Input type="text" id="modal-note" bind:value={newPositionData.note} />

    {#snippet footer()}
      <Button color="light" onclick={pushNewPosition}>Add</Button>
    {/snippet}
  </Modal>
</div>
