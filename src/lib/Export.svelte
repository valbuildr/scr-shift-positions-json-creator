<script lang="ts">
  import type {
    DriverPositionInfo,
    DispatcherPositionInfo,
    GuardPositionInfo,
    SignallerPositionInfo,
    SupervisorPositionInfo,
  } from "$lib";

  let {
    qdPos = undefined,
    dsPos = undefined,
    gdPos = undefined,
    sgPos = undefined,
    svPos = undefined,
  }: {
    qdPos?: DriverPositionInfo[];
    dsPos?: DispatcherPositionInfo[];
    gdPos?: GuardPositionInfo[];
    sgPos?: SignallerPositionInfo[];
    svPos?: SupervisorPositionInfo[];
  } = $props();

  import { Button } from "flowbite-svelte";

  let full = {
    driver: qdPos,
    dispatcher: dsPos,
    guard: gdPos,
    signaller: sgPos,
    supervisor: svPos,
  };
</script>

<div
  class="bg-slate-700 max-w-screen-xl mx-auto rounded-tl-none rounded-xl p-4 text-white mb-4 dark"
>
  <Button
    color="light"
    onclick={() => {
      const dataStr =
        "data:text/json;charset=utf-8," +
        encodeURIComponent(JSON.stringify(full, null, 2));
      const dlAnchorElem = document.createElement("a");
      dlAnchorElem.setAttribute("href", dataStr);
      dlAnchorElem.setAttribute("download", "positions.json");
      document.body.appendChild(dlAnchorElem);
      dlAnchorElem.click();
      document.body.removeChild(dlAnchorElem);
    }}
  >
    Export
  </Button>
</div>
