<script>
import { Base64 } from 'js-base64';
import TextArea from '$lib/suil/TextArea.svelte';
import Code from '$lib/suil/Code.svelte';

let value = $state('');
</script>

<div class="space-y-4 p-4">
  <div><TextArea placeholder="Enter text to encode" bind:value /></div>
  <Code placeholder="Base64 encoded string" code={Base64.encode(value)} />
</div>
