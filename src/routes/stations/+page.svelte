<script lang="ts">
  import { stations, Operator, SignalZone } from "$lib";
</script>

<div class="p-8 bg-gray-800 text-white min-h-screen">
  {#each Object.entries(stations) as station}
    <div>
      <div class="flex items-center gap-3">
        {#if station[1].managers[0] == Operator.Airlink}
          <p class="text-2xl font-bold p-1.5 bg-airlink text-white rounded-md">
            {station[0]}
          </p>
        {:else if station[1].managers[0] == Operator.Connect}
          <p class="text-2xl font-bold p-1.5 bg-connect text-white rounded-md">
            {station[0]}
          </p>
        {:else if station[1].managers[0] == Operator.Express}
          <p class="text-2xl font-bold p-1.5 bg-express text-white rounded-md">
            {station[0]}
          </p>
        {:else if station[1].managers[0] == Operator.Waterline}
          <p
            class="text-2xl font-bold p-1.5 bg-waterline text-white rounded-md"
          >
            {station[0]}
          </p>
        {:else if station[1].managers[0] == Operator.Metro}
          <p class="text-2xl font-bold p-1.5 bg-metro text-white rounded-md">
            {station[0]}
          </p>
        {:else if station[1].managers[0] == Operator.NationalRail}
          <p class="text-2xl font-bold p-1.5 bg-blue-900 text-white rounded-md">
            {station[0]}
          </p>
        {:else if station[1].managers[0] == Operator.TransportForStepford}
          <p class="text-2xl font-bold p-1.5 bg-black text-white rounded-md">
            {station[0]}
          </p>
        {/if}

        <p class="text-2xl">
          {station[1].name}
        </p>

        {#if station[1].operators.includes(Operator.Airlink)}
          <p class="p-1.5 bg-airlink text-white rounded-md">Airlink</p>
        {/if}
        {#if station[1].operators.includes(Operator.Connect)}
          <p class="p-1.5 bg-connect text-white rounded-md">Connect</p>
        {/if}
        {#if station[1].operators.includes(Operator.Express)}
          <p class="p-1.5 bg-express text-white rounded-md">Express</p>
        {/if}
        {#if station[1].operators.includes(Operator.Waterline)}
          <p class="p-1.5 bg-waterline text-white rounded-md">Waterline</p>
        {/if}
        {#if station[1].operators.includes(Operator.Metro)}
          <p class="p-1.5 bg-metro text-white rounded-md">Metro</p>
        {/if}
      </div>

      <p class="text-xl">Managers</p>
      {#each station[1].managers as manager}
        {#if manager == Operator.Airlink}
          <p>Airlink</p>
        {:else if manager == Operator.Connect}
          <p>Connect</p>
        {:else if manager == Operator.Express}
          <p>Express</p>
        {:else if manager == Operator.Waterline}
          <p>Waterline</p>
        {:else if manager == Operator.Metro}
          <p>Metro</p>
        {:else if manager == Operator.NationalRail}
          <p>National Rail</p>
        {:else if manager == Operator.TransportForStepford}
          <p>Transport for Stepford</p>
        {/if}
      {/each}

      <p class="text-xl">Platforms</p>

      <div class="flex gap-1">
        {#each station[1].platforms as platform}
          <p>{platform}</p>
        {/each}
      </div>

      <p class="text-xl">Signal Zone(s)</p>

      {#each station[1].signalZone as zone}
        {#if zone == SignalZone.A}
          <p>A</p>
        {:else if zone == SignalZone.B}
          <p>B</p>
        {:else if zone == SignalZone.C}
          <p>C</p>
        {:else if zone == SignalZone.D}
          <p>D</p>
        {:else if zone == SignalZone.E}
          <p>E</p>
        {:else if zone == SignalZone.F}
          <p>F</p>
        {:else if zone == SignalZone.G}
          <p>G</p>
        {:else if zone == SignalZone.H}
          <p>H</p>
        {:else if zone == SignalZone.J}
          <p>J</p>
        {/if}
      {/each}

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
