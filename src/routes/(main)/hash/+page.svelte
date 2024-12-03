<script>
import md5 from 'crypto-js/md5';
import sha1 from 'crypto-js/sha1';
import sha256 from 'crypto-js/sha256';
import sha512 from 'crypto-js/sha512';
import TextArea from '$lib/suil/TextArea.svelte';
import Tabs from '$lib/suil/Tabs.svelte';
import TabsButton from '$lib/suil/TabsButton.svelte';
import Code from '$lib/suil/Code.svelte';

const TYPES = [
  { name: 'MD5', func: md5 },
  { name: 'SHA-1', func: sha1 },
  { name: 'SHA-256', func: sha256 },
  { name: 'SHA-512', func: sha512 },
];

let value = $state('');
let hashName = $state(TYPES[1].name);
let hashType = $derived(TYPES.find((x) => x.name === hashName));
</script>

<div class="space-y-4 p-4">
  <div><TextArea placeholder="Enter text to hash" bind:value /></div>

  <div class="flex flex-row justify-start">
    <Tabs bind:value={hashName}>
      {#each TYPES as item (item.name)}
        <TabsButton name={item.name}>{item.name}</TabsButton>
      {/each}
    </Tabs>
  </div>

  <Code placeholder="Hashed string" code={hashType.func(value).toString()} />
</div>
