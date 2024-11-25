<script>
import '$lib/styles/app.css';
import { page } from '$app/stores';

let { children } = $props();
</script>

<div class="max-w-container mx-auto flex min-h-screen flex-row">
  {@render children()}
</div>
