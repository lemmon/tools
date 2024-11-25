<script>
import * as uuid from 'uuid';
import Button from '$lib/suil/Button.svelte';
import TextInput from '$lib/suil/TextInput.svelte';
import CopyButton from '$lib/suil/CopyButton.svelte';
import Dump from '$lib/suil/Dump.svelte';

import MagicWandIcon from 'carbon-icons-svelte/lib/MagicWand.svelte';

let value = $state('');
let valid = $derived(uuid.validate(value));
let version = $derived(valid && uuid.version(value));
</script>

<div class="space-y-4 p-4">
  <div class="flex flex-row items-center gap-2">
    <div class="flex flex-row items-center gap-1 text-current/60">
      <MagicWandIcon />
      Generate
    </div>
    <div class="flex flex-row items-center gap-1">
      <Button class="suil-size-xs" onclick={() => (value = uuid.v1())}>UUID v1</Button>
      <Button class="suil-size-xs" onclick={() => (value = uuid.v4())}>UUID v4</Button>
      <Button class="suil-size-xs" onclick={() => (value = uuid.v6())}>UUID v6</Button>
      <Button class="suil-size-xs" onclick={() => (value = uuid.v7())}>UUID v7</Button>
    </div>
  </div>
  <TextInput placeholder="Enter UUID" bind:value>
    {#snippet after()}
      <CopyButton class="suil-button-inset" kind="ghost" text={value} />
    {/snippet}
  </TextInput>
  <Dump data={{ valid, version }} />
</div>
