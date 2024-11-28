<script>
import * as uuid from 'uuid';
import Button from '$lib/suil/Button.svelte';
import Code from '$lib/suil/Code.svelte';
import TextInput from '$lib/suil/TextInput.svelte';
import CopyButton from '$lib/suil/CopyButton.svelte';

import MagicWandIcon from 'carbon-icons-svelte/lib/MagicWand.svelte';

let value = $state('');
let length = $state(16);
let index = $state(1);

$effect(() => {
  value = generateSecurePassword(length);
  index;
});

function generateSecurePassword(length = 12) {
  const characters =
    'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()_+[]{}|;:,.<>?';
  const charactersLength = characters.length;
  let password = '';

  // Generate a secure array of random values
  const randomValues = new Uint8Array(length);
  window.crypto.getRandomValues(randomValues);

  // Map random values to characters
  for (let i = 0; i < length; i++) {
    password += characters[randomValues[i] % charactersLength];
  }

  return password;
}
</script>

<div class="space-y-4 p-4">
  <header>
    <h1 class="text-2xl">Secure Password Generator</h1>
  </header>
  <Code code={value} />
  <div class="flex flex-row items-center gap-1">
    <Button class="suil-size-xs" onclick={() => index++}><MagicWandIcon /> Generate</Button>
  </div>
</div>
