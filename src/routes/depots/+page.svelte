<script lang="ts">
  import { routes } from "$lib";
</script>

<div class="p-8 bg-gray-800 text-white min-h-screen">
  {#each Object.entries(routes) as route}
    <div>
      <div class="flex items-center gap-3">
        {#if route[1].operator == 0}
          <p class="text-2xl font-bold p-1.5 bg-airlink text-white rounded-md">
            {route[0]}
          </p>
        {:else if route[1].operator == 1}
          <p class="text-2xl font-bold p-1.5 bg-connect text-white rounded-md">
            {route[0]}
          </p>
        {:else if route[1].operator == 2}
          <p class="text-2xl font-bold p-1.5 bg-express text-white rounded-md">
            {route[0]}
          </p>
        {:else if route[1].operator == 3}
          <p
            class="text-2xl font-bold p-1.5 bg-waterline text-white rounded-md"
          >
            {route[0]}
          </p>
        {:else if route[1].operator == 4}
          <p class="text-2xl font-bold p-1.5 bg-metro text-white rounded-md">
            {route[0]}
          </p>
        {/if}

        <p class="text-2xl">
          {route[1].inboundDestination} &lt;&gt; {route[1].outboundDestination}
        </p>

        {#if route[1].altName}
          <p class="text-xl">"{route[1].altName}"</p>
        {/if}
      </div>

      {#if route[1].inboundDepots}
        <p class="text-xl">Inbound (towards {route[1].inboundDestination})</p>
        {#each route[1].inboundDepots as depot}
          <p>{depot}</p>
        {/each}
      {/if}

      {#if route[1].outboundDepots}
        <p class="text-xl">Outbound (towards {route[1].outboundDestination})</p>
        {#each route[1].outboundDepots as depot}
          <p>{depot}</p>
        {/each}
      {/if}
    </div>

    <hr class="my-4 border border-gray-700" />
  {/each}
</div>
