<script lang="ts">
  import { stations } from "$lib";
</script>

<div class="p-8 bg-gray-800 text-white min-h-screen">
  {#each Object.entries(stations) as station}
    <div>
      <div class="flex items-center gap-3">
        {#if station[1].managers[0] == 0}
          <p class="text-2xl font-bold p-1.5 bg-airlink text-white rounded-md">
            {station[0]}
          </p>
        {:else if station[1].managers[0] == 1}
          <p class="text-2xl font-bold p-1.5 bg-connect text-white rounded-md">
            {station[0]}
          </p>
        {:else if station[1].managers[0] == 2}
          <p class="text-2xl font-bold p-1.5 bg-express text-white rounded-md">
            {station[0]}
          </p>
        {:else if station[1].managers[0] == 3}
          <p
            class="text-2xl font-bold p-1.5 bg-waterline text-white rounded-md"
          >
            {station[0]}
          </p>
        {:else if station[1].managers[0] == 4}
          <p class="text-2xl font-bold p-1.5 bg-metro text-white rounded-md">
            {station[0]}
          </p>
        {:else if station[1].managers[0] == 5}
          <p class="text-2xl font-bold p-1.5 bg-blue-900 text-white rounded-md">
            {station[0]}
          </p>
        {/if}

        <p class="text-2xl">
          {station[1].name}
        </p>

        {#if station[1].operators.includes(0)}
          <p class="p-1.5 bg-airlink text-white rounded-md">Airlink</p>
        {/if}
        {#if station[1].operators.includes(1)}
          <p class="p-1.5 bg-connect text-white rounded-md">Connect</p>
        {/if}
        {#if station[1].operators.includes(2)}
          <p class="p-1.5 bg-express text-white rounded-md">Express</p>
        {/if}
        {#if station[1].operators.includes(3)}
          <p class="p-1.5 bg-waterline text-white rounded-md">Waterline</p>
        {/if}
        {#if station[1].operators.includes(4)}
          <p class="p-1.5 bg-metro text-white rounded-md">Metro</p>
        {/if}
      </div>

      <p class="text-xl">Managers</p>
      {#each station[1].managers as manager}
        {#if manager == 0}
          <p>Airlink</p>
        {:else if manager == 1}
          <p>Connect</p>
        {:else if manager == 2}
          <p>Express</p>
        {:else if manager == 3}
          <p>Waterline</p>
        {:else if manager == 4}
          <p>Metro</p>
        {:else if manager == 5}
          <p>National Rail</p>
        {:else if manager == 6}
          <p>Transport for Stepford</p>
        {/if}
      {/each}

      <p class="text-xl">Platforms</p>

      <div class="flex gap-1">
        {#each station[1].platforms as platform}
          <p>{platform}</p>
        {/each}
      </div>

      <p class="text-xl">Signal Zone</p>

      {#if station[1].signalZone == 0}
        <p>A</p>
      {:else if station[1].signalZone == 1}
        <p>B</p>
      {:else if station[1].signalZone == 2}
        <p>C</p>
      {:else if station[1].signalZone == 3}
        <p>D</p>
      {:else if station[1].signalZone == 4}
        <p>E</p>
      {:else if station[1].signalZone == 5}
        <p>F</p>
      {:else if station[1].signalZone == 6}
        <p>G</p>
      {:else if station[1].signalZone == 7}
        <p>H</p>
      {:else if station[1].signalZone == 8}
        <p>J</p>
      {/if}

      {#if station[1].dsGroups}
        <p class="text-xl">Dispatch Groups</p>

        {#each station[1].dsGroups as group}
          <div class="flex gap-1">
            {#each group as platform}
              <p>{platform}</p>
            {/each}
          </div>
        {/each}
      {/if}
    </div>

    <hr class="my-4 border border-gray-700" />
  {/each}
</div>
