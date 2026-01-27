<script lang="ts">
  // 1. 定义属性 (Props)
  // 确保这里的变量名是 bgColor，注意 C 是大写
  export let label: string = "Button";
  export let bgColor: string = "bg-blue-600"; // 默认背景颜色
  export let onClick: () => void = () => {};  // 默认点击函数
</script>

<button
  on:click={onClick}
  class="{bgColor} text-white font-bold py-2 px-6 rounded-lg 
         transition-all duration-200 transform
         hover:brightness-110 hover:scale-105
         focus:outline-none focus:ring-4 focus:ring-blue-300
         active:scale-95 active:shadow-inner"
>
  {label}
</button>

<style>
  /* 这里的样式通常留空，因为我们主要使用 Tailwind */
</style>