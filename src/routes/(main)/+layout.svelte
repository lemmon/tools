<script>
import { page } from '$app/stores';

let { children } = $props();

const nav = [
  { href: '/base64', label: 'Base64' },
  { href: '/md5', label: 'MD5' },
  { href: '/uuid', label: 'UUID' },
];
</script>

<nav class="my-4 flex w-72 flex-col border-r border-neutral-200">
  <ul class="flex-1 space-y-px px-4 leading-tight">
    {#each nav as { href, label } (href)}
      <li>
        <a
          class="block rounded-md p-3 {href === $page.url.pathname
            ? 'bg-neutral-300/30'
            : 'hover:bg-neutral-300/30'}"
          {href}>{label}</a
        >
      </li>
    {/each}
  </ul>
</nav>

<main class="flex flex-1 flex-col">
  {@render children()}
</main>
