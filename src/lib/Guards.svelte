<script lang="ts">
  import type { GuardPositionInfo } from "$lib";

  import { Button, Modal, Label, Input } from "flowbite-svelte";

  let { positions = $bindable() }: { positions: GuardPositionInfo[] } =
    $props();

  let showModal: boolean = $state(false);
  let newPositionData: GuardPositionInfo = $state({ id: "" });

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
    <p class="text-2xl p-1.5 bg-gd w-fit rounded-xl font-medium">GD</p>
    <p class="text-2xl">Guard Positions</p>

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
        class="bg-slate-600 border border-slate-500 rounded-xl rounded-tl-none mt-2 p-2 grid grid-cols-6 items-center"
      >
        <p>{pos.id}</p>
        <p>{pos.train ? pos.train : "Any train"}</p>
        <p>{pos.player ? pos.player : "Any player"}</p>
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

  <Modal title="New Guard Position" bind:open={showModal}>
    <Label for="modal-id" class="ml-1 mb-2">ID</Label>
    <Input
      type="number"
      id="modal-id"
      class="mb-2"
      min="1"
      bind:value={newPositionData.id}
    />

    <Label for="modal-train" class="ml-1 mb-2">Train</Label>
    <Input
      type="text"
      id="modal-train"
      class="mb-2"
      bind:value={newPositionData.train}
    />

    <Label for="modal-player" class="ml-1 mb-2">Player</Label>
    <Input
      type="text"
      id="modal-player"
      class="mb-2"
      bind:value={newPositionData.player}
    />

    <Label for="modal-note" class="ml-1 mb-2">Note</Label>
    <Input type="text" id="modal-note" bind:value={newPositionData.note} />

    {#snippet footer()}
      <Button color="light" onclick={pushNewPosition}>Add</Button>
    {/snippet}
  </Modal>
</div>
