<script lang="ts">
  import type { DriverPositionInfo } from "$lib";
  import { routes } from "$lib";

  import { Button, Modal, Label, Input, Select } from "flowbite-svelte";

  let { positions = $bindable() }: { positions: DriverPositionInfo[] } =
    $props();

  let showModal: boolean = $state(false);
  let newPositionData: DriverPositionInfo = $state({ id: "" });

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

  let formattedRoutes: { value: string; name: string }[] = [];
  for (const route of Object.entries(routes)) {
    if (route[1].altName) {
      formattedRoutes.push({
        value: route[0],
        name: `${route[0]}: ${route[1].altName} (${route[1].inboundDestination} <> ${route[1].outboundDestination})`,
      });
    } else {
      formattedRoutes.push({
        value: route[0],
        name: `${route[0]}: ${route[1].inboundDestination} <> ${route[1].outboundDestination}`,
      });
    }
  }

  let depots: { value: string; name: string }[] = $state([]);
  const updateDepots = () => {
    depots = [];

    const routeData =
      routes[newPositionData.route ? newPositionData.route : "R001"];

    for (const depot of routeData.inboundDepots
      ? routeData.inboundDepots
      : []) {
      depots.push({
        value: depot,
        name: `${depot} (towards ${routeData.inboundDestination})`,
      });
    }
    for (const depot of routeData.outboundDepots
      ? routeData.outboundDepots
      : []) {
      depots.push({
        value: depot,
        name: `${depot} (towards ${routeData.outboundDestination})`,
      });
    }
  };
</script>

<div
  class="bg-slate-700 max-w-screen-xl mx-auto rounded-tl-none rounded-xl p-4 text-white mb-4 dark"
>
  <div class="flex gap-2 items-center">
    <p class="text-2xl p-1.5 bg-qd w-fit rounded-xl font-medium">QD</p>
    <p class="text-2xl">Driver Positions</p>

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
      <p>No driver positions added.</p>
    </div>
  {:else}
    {#each positions as pos}
      <div
        class="bg-slate-600 border border-slate-500 rounded-xl rounded-tl-none mt-2 p-2 grid grid-cols-6 items-center"
      >
        <p>{pos.id}</p>
        <p>{pos.route ? pos.route : "Any route"}</p>
        <p>{pos.depot ? pos.depot : "Any depot"}</p>
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

  <Modal title="New Driver Position" bind:open={showModal}>
    <Label for="modal-id" class="ml-1 mb-2">ID</Label>
    <Input
      type="number"
      id="modal-id"
      class="mb-2"
      min="1"
      bind:value={newPositionData.id}
    />

    <Label for="modal-route" class="ml-1 mb-2">Route</Label>
    <Select
      id="modal-route"
      class="mb-2"
      bind:value={newPositionData.route}
      items={formattedRoutes}
      onchange={updateDepots}
    />

    <Label for="modal-depot" class="ml-1 mb-2">Depot</Label>
    <Select
      id="modal-depot"
      class="mb-2"
      bind:value={newPositionData.depot}
      items={depots}
      disabled={newPositionData.route == undefined}
    />

    <Label for="modal-note" class="ml-1 mb-2">Note</Label>
    <Input type="text" id="modal-note" bind:value={newPositionData.note} />

    {#snippet footer()}
      <Button color="light" onclick={pushNewPosition}>Add</Button>
    {/snippet}
  </Modal>
</div>
