<script>
import '../app.css';
import { page } from '$app/stores';

let { children } = $props();

const nav = [{ href: '/uuid', label: 'UUID' }];
</script>

<div class="max-w-container mx-auto flex min-h-screen flex-row">
  <nav class="my-3 flex w-72 flex-col border-r border-neutral-200">
    <ul class="flex-1 rounded-lg px-3">
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
</div>
