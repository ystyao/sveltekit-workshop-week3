<script lang="ts">
  // 1. 引入你在 Task 1 封装好的组件
  import Button from '$lib/Button.svelte';

  // 2. 定义数据数组 (Grocery List)
  let groceryList = [
    { id: 1, name: 'Organic Eggs', category: 'Dairy', price: 5.99, color: 'bg-amber-500' },
    { id: 2, name: 'Sourdough Bread', category: 'Bakery', price: 4.50, color: 'bg-orange-500' },
    { id: 3, name: 'Whole Milk', category: 'Dairy', price: 3.25, color: 'bg-sky-500' },
    { id: 4, name: 'Honey Crispy Apples', category: 'Produce', price: 2.80, color: 'bg-rose-500' },
    { id: 5, name: 'Blueberries', category: 'Produce', price: 6.50, color: 'bg-indigo-500' },
  ];

  // 3. 点击交互逻辑
  const handlePurchase = (name: string) => {
    alert(`Added ${name} to your virtual cart! 🛒`);
  };
</script>

<main class="min-h-screen bg-slate-50 py-12 px-4 flex flex-col items-center">
  
  <div class="max-w-md w-full">
    <header class="mb-10 text-center">
      <span class="text-emerald-600 font-bold tracking-widest text-sm uppercase">Workshop Week 3</span>
      <h1 class="text-4xl font-black text-slate-900 mt-2">Inventory</h1>
    </header>

    <div class="bg-white shadow-2xl rounded-3xl overflow-hidden border border-slate-100">
      <ul class="divide-y divide-slate-100">
        
        {#each groceryList as item (item.id)}
          <li class="p-6 flex items-center justify-between hover:bg-slate-50 transition-colors group">
            
            <div class="flex items-center gap-4">
              <div class="w-1.5 h-12 rounded-full {item.color}"></div>
              
              <div>
                <p class="font-bold text-slate-800 text-lg">{item.name}</p>
                <p class="text-xs font-semibold text-slate-400 uppercase tracking-tighter">
                  {item.category}
                </p>
              </div>
            </div>

            <div class="flex items-center gap-5">
              <span class="font-mono font-bold text-slate-500">
                ${item.price.toFixed(2)}
              </span>

              <Button 
                label="Get" 
                bgColor={item.color} 
                onClick={() => handlePurchase(item.name)} 
              />
            </div>

          </li>
        {/each}

      </ul>
    </div>

    <p class="mt-6 text-center text-slate-400 text-sm italic">
      Showing {groceryList.length} items from the local database
    </p>
  </div>

</main>