<script>
import { Base64 } from 'js-base64';
import TextArea from '$lib/suil/TextArea.svelte';
import Tabs from '$lib/suil/Tabs.svelte';
import TabsButton from '$lib/suil/TabsButton.svelte';
import Code from '$lib/suil/Code.svelte';

import WarningFilledIcon from 'carbon-icons-svelte/lib/WarningFilled.svelte';

const ACTIONS = ['encode', 'decode'];

let value = $state('');
let action = $state('encode');
let result = $derived.by(() => {
  try {
    if (action === 'decode' && !Base64.isValid(value)) throw new Error('Invalid Input');
    return Base64[action](value);
  } catch (error) {
    return -1;
  }
});
</script>

<div class="space-y-4 p-4">
  <div><TextArea placeholder="Enter text to {action}" bind:value /></div>

  <div class="flex flex-row justify-start">
    <Tabs bind:value={action}>
      {#each ACTIONS as item (item)}
        <TabsButton name={item}>{item}</TabsButton>
      {/each}
    </Tabs>
  </div>

  {#if result !== -1}
    <Code placeholder="Base64 {action}d string" code={result} />
  {:else}
    <div class="flex flex-row items-center gap-1 rounded-md bg-red-100 p-4 leading-5 text-red-600">
      <WarningFilledIcon class="m-0.5" />
      Invalid Input
    </div>
  {/if}
</div>
