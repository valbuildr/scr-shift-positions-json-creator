<script lang="ts">
  import { signal_zones, type SignallerPositionInfo } from "$lib";

  import { Button, Modal, Label, Input, Select } from "flowbite-svelte";

  let { positions = $bindable() }: { positions: SignallerPositionInfo[] } =
    $props();

  let showModal: boolean = $state(false);
  let newPositionData: SignallerPositionInfo = $state({ id: "" });

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

  let zones: { value: string; name: string }[] = [];
  for (const zone of Object.entries(signal_zones)) {
    zones.push({ value: zone[0], name: `${zone[0]}: ${zone[1].name}` });
  }
</script>

<div
  class="bg-slate-700 max-w-screen-xl mx-auto rounded-tl-none rounded-xl p-4 text-white mb-4 dark"
>
  <div class="flex gap-2 items-center">
    <p class="text-2xl p-1.5 bg-sg w-fit rounded-xl font-medium">SG</p>
    <p class="text-2xl">Signaller Positions</p>

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
      <p>No guard positions added.</p>
    </div>
  {:else}
    {#each positions as pos}
      <div
        class="bg-slate-600 border border-slate-500 rounded-xl rounded-tl-none mt-2 p-2 grid grid-cols-5 items-center"
      >
        <p>{pos.id}</p>
        <p>{pos.zone ? pos.zone : "Any zone"}</p>
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

  <Modal title="New Signaller Position" bind:open={showModal}>
    <Label for="modal-id" class="ml-1 mb-2">ID</Label>
    <Input
      type="number"
      id="modal-id"
      class="mb-2"
      min="1"
      bind:value={newPositionData.id}
    />

    <Label for="modal-zone" class="ml-1 mb-2">Zone</Label>
    <Select
      id="modal-zone"
      class="mb-2"
      bind:value={newPositionData.zone}
      items={zones}
    />

    <Label for="modal-note" class="ml-1 mb-2">Note</Label>
    <Input type="text" id="modal-note" bind:value={newPositionData.note} />

    {#snippet footer()}
      <Button color="light" onclick={pushNewPosition}>Add</Button>
    {/snippet}
  </Modal>
</div>
