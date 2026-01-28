<script lang="ts">
  import { onMount } from 'svelte';
  import Button from '$lib/Button.svelte';

  // --- Task 2: 本地数据 (保持不变) ---
  let groceryList = [
    { id: 1, name: 'Organic Eggs', category: 'Dairy', price: 5.99, color: 'bg-amber-500' },
    { id: 2, name: 'Sourdough Bread', category: 'Bakery', price: 4.50, color: 'bg-orange-500' },
    { id: 3, name: 'Whole Milk', category: 'Dairy', price: 3.25, color: 'bg-sky-500' },
    { id: 4, name: 'Honey Crispy Apples', category: 'Produce', price: 2.80, color: 'bg-rose-500' },
    { id: 5, name: 'Blueberries', category: 'Produce', price: 6.50, color: 'bg-indigo-500' },
    // 以下是新增加的补给品
    { id: 6, name: 'Freeze-Dried Ice Cream', category: 'Ration', price: 12.00, color: 'bg-purple-500' },
    { id: 7, name: 'Oxygen Canisters', category: 'Survival', price: 25.00, color: 'bg-teal-400' },
    { id: 8, name: 'Space Coffee Beans', category: 'Ration', price: 8.50, color: 'bg-yellow-600' }
  ];

  // --- Task 3: API 异步数据 (Star Wars 叙事版) ---
  let characters = [];
  let loading = true;
  let error = null;

  async function fetchGalacticArchive() {
    try {
      loading = true;
      // 抓取星球大战人物数据
      const response = await fetch('https://swapi.dev/api/people/');
      if (!response.ok) throw new Error('Holonet Connection Interrupted');
      const data = await response.json();
      characters = data.results.slice(0, 5); // 只取前5个英雄
    } catch (e) {
      error = e.message;
    } finally {
      loading = false;
    }
  }

  onMount(fetchGalacticArchive);
</script>

<main class="min-h-screen bg-slate-900 py-12 px-4 flex flex-col items-center gap-12 text-slate-100">
  
  <section class="max-w-md w-full">
    <div class="flex items-center gap-3 mb-6">
      <span class="text-2xl">🍎</span>
      <h2 class="text-xl font-bold tracking-tighter text-amber-400 uppercase">Space Rations (Local)</h2>
    </div>

    <div class="bg-slate-800 rounded-3xl overflow-hidden border border-slate-700 shadow-2xl">
      {#each groceryList as item}
        <div class="p-4 flex justify-between items-center border-b border-slate-700 last:border-0">
          <span class="font-medium">{item.name}</span>
          <Button label="Stock" bgColor={item.color} onClick={() => alert(`Replenishing ${item.name}`)} />
        </div>
      {/each}
    </div>
  </section>

  <div class="w-full max-w-md h-px bg-gradient-to-r from-transparent via-blue-500 to-transparent opacity-30"></div>

  <section class="max-w-md w-full">
    <div class="flex items-center gap-3 mb-6">
      <span class="text-2xl animate-pulse">🛸</span>
      <h2 class="text-xl font-bold tracking-tighter text-blue-400 uppercase">Galactic Registry (API)</h2>
    </div>

    {#if loading}
      <div class="bg-slate-800 p-10 rounded-3xl border border-blue-900/50 text-center flex flex-col items-center">
        <div class="w-12 h-12 border-4 border-blue-500/20 border-t-blue-500 rounded-full animate-spin mb-4"></div>
        <p class="text-blue-400 font-mono text-sm uppercase tracking-widest">Scanning Outer Rim...</p>
      </div>
    {:else if error}
      <div class="bg-red-900/20 p-6 rounded-3xl border border-red-500/50 text-center">
        <p class="text-red-400 font-bold">Signal Lost: {error}</p>
        <button on:click={fetchGalacticArchive} class="mt-4 text-xs uppercase tracking-widest text-red-300 underline">Re-establish Uplink</button>
      </div>
    {:else}
      <div class="space-y-4">
        {#each characters as person}
          <div class="bg-slate-800 p-5 rounded-2xl border border-slate-700 hover:border-blue-500/50 transition-all group shadow-lg">
            <div class="flex justify-between items-start">
              <div>
                <h3 class="font-black text-lg text-white group-hover:text-blue-300 transition-colors uppercase tracking-tight">
                  {person.name}
                </h3>
                <div class="flex gap-2 mt-1">
                  <span class="text-[10px] bg-slate-700 px-2 py-0.5 rounded text-slate-300 uppercase">Height: {person.height}cm</span>
                  <span class="text-[10px] bg-slate-700 px-2 py-0.5 rounded text-slate-300 uppercase">Mass: {person.mass}kg</span>
                </div>
              </div>
              <Button label="Profile" bgColor="bg-blue-600" onClick={() => alert(`Accessing classified files for ${person.name}...`)} />
            </div>
          </div>
        {/each}
      </div>
    {/if}
  </section>

</main>