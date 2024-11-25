<script>
import md5 from 'md5';
import TextArea from '$lib/suil/TextArea.svelte';
import Code from '$lib/suil/Code.svelte';

let value = $state('');
</script>

<div class="space-y-4 p-4">
  <div><TextArea placeholder="Enter text to hash" bind:value /></div>
  <Code placeholder="Hashed string" code={value && md5(value)} />
</div>
