<script lang="ts">
  import type { SupervisorPositionInfo } from "$lib";

  import { Button, Modal, Label, Input, Select } from "flowbite-svelte";

  let { positions = $bindable() }: { positions: SupervisorPositionInfo[] } =
    $props();

  let showModal: boolean = $state(false);
  let newPositionData: SupervisorPositionInfo = $state({ id: "" });

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
</script>

<div
  class="bg-slate-700 max-w-screen-xl mx-auto rounded-tl-none rounded-xl p-4 text-white mb-4 dark"
>
  <div class="flex gap-2 items-center">
    <p class="text-2xl p-1.5 bg-sv w-fit rounded-xl font-medium">SV</p>
    <p class="text-2xl">Supervisor Positions</p>

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
      <p>
        No supervisor positions added. <b
          >You must have at least one. Make sure to add one for yourself!</b
        >
      </p>
    </div>
  {:else}
    {#each positions as pos}
      <div
        class="bg-slate-600 border border-slate-500 rounded-xl rounded-tl-none mt-2 p-2 grid grid-cols-4 items-center"
      >
        <p>{pos.id}</p>
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

  <Modal title="New Supervisor Position" bind:open={showModal}>
    <Label for="modal-id" class="ml-1 mb-2">ID</Label>
    <Input
      type="number"
      id="modal-id"
      class="mb-2"
      min="1"
      bind:value={newPositionData.id}
    />

    <Label for="modal-note" class="ml-1 mb-2">Note</Label>
    <Input type="text" id="modal-note" bind:value={newPositionData.note} />

    {#snippet footer()}
      <Button color="light" onclick={pushNewPosition}>Add</Button>
    {/snippet}
  </Modal>
</div>
