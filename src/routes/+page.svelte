<script lang="ts">
  // 1. 引入你的 Button 组件
  import Button from '$lib/Button.svelte';

  // 2. 定义简单的交互函数（Task 1 要求有交互）
  const handleSuccess = () => alert("Success: Changes Saved!");
  const handleDanger  = () => alert("Danger: Item Deleted!");
  const handleInfo    = () => alert("Info: Starting Upload...");
</script>

<main class="min-h-screen flex flex-col items-center justify-center bg-gray-50 p-4">
  
  <div class="mb-12 text-center">
    <h1 class="text-4xl font-black text-gray-900 tracking-tight">
      SvelteKit Workshop
    </h1>
    <p class="text-gray-500 mt-2 text-lg">Task 1: Reusable Components & Tailwind v4</p>
  </div>

  <div class="flex flex-wrap gap-6 justify-center">
    
    <Button 
      label="Save" 
      bgColor="bg-emerald-500" 
      onClick={handleSuccess} 
    />

    <Button 
      label="Delete" 
      bgColor="bg-rose-500" 
      onClick={handleDanger} 
    />

    <Button 
      label="Upload" 
      bgColor="bg-blue-600" 
      onClick={handleInfo} 
    />

  </div>

  <div class="mt-12 p-4 bg-blue-50 rounded-lg border border-blue-100 text-sm text-blue-700">
    <strong>检查点：</strong> how you gonna do with the buttons?
  </div>

</main>