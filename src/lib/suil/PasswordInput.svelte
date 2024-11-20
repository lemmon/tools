<script>
// Global Stylesheet
import './styles.css';

// Local Dependencies
import Button from './Button.svelte';
import TextInput from './TextInput.svelte';

// Icons
import ViewIcon from 'carbon-icons-svelte/lib/View.svelte';
import ViewOffIcon from 'carbon-icons-svelte/lib/ViewOff.svelte';

//

let { value = $bindable(), visible = $bindable(false), header, footer, ...props } = $props();
let Icon = $derived(visible ? ViewIcon : ViewOffIcon);
</script>

{#snippet fieldFooter()}{@render footer?.({ value, visible })}{/snippet}

<TextInput
  {...props}
  footer={footer && fieldFooter}
  type={visible ? 'text' : 'password'}
  bind:value
>
  {#snippet after()}
    <div>
      <Button
        type="button"
        class="suil-button-inset"
        kind="ghost"
        onclick={() => {
          visible = !visible;
        }}><Icon class="suil-icon" /></Button
      >
    </div>
  {/snippet}
</TextInput>
