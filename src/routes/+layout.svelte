<script>
import '../app.css';

let { children } = $props();
</script>

<div class="max-w-container mx-auto flex min-h-screen flex-col">
  {@render children()}
</div>
