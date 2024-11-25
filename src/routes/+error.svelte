<script>
import { page } from '$app/stores';
import Button from '$lib/suil/Button.svelte';
</script>

<div class="m-auto space-y-8 p-8">
  <header>
    <h1 class="text-5xl tracking-tight">{$page.status} {$page.error.message}</h1>
  </header>
  <div class="flex-flex flex flex-row justify-center gap-2">
    <Button class="suil-pill suil-gutter" href="/">Return Home</Button>
  </div>
</div>
