<script>
import md5 from 'crypto-js/md5';
import sha1 from 'crypto-js/sha1';
import sha256 from 'crypto-js/sha256';
import sha512 from 'crypto-js/sha512';
import Button from '$lib/suil/Button.svelte';
import TextArea from '$lib/suil/TextArea.svelte';
import Code from '$lib/suil/Code.svelte';

const TYPES = [
  { name: 'MD5', func: md5 },
  { name: 'SHA-1', func: sha1 },
  { name: 'SHA-256', func: sha256 },
  { name: 'SHA-512', func: sha512 },
];

let value = $state('');
let hashType = $state(TYPES[0]);
</script>

<div class="space-y-4 p-4">
  <div><TextArea placeholder="Enter text to hash" bind:value /></div>

  <div class="flex flex-row justify-start">
    <div class="flex flex-row gap-px rounded-md bg-neutral-100 p-0.5">
      {#each TYPES as item (item.name)}
        <Button
          class="suil-size-xs suil-gutter rounded-sm"
          type="button"
          kind={item.name !== hashType.name && 'ghost'}
          onclick={() => (hashType = item)}>{item.name}</Button
        >
      {/each}
    </div>
  </div>

  <Code placeholder="Hashed string" code={hashType.func(value).toString()} />
</div>
