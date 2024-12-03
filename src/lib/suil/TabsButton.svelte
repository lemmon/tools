<script>
import { getContext } from 'svelte';
import Button from './Button.svelte';

let { name, children, ...props } = $props();

const selected = getContext('selected');
</script>

<Button
  type="button"
  kind="ghost"
  {...props}
  data-selected={name === selected.value || undefined}
  onclick={() => (selected.value = name)}>{@render children()}</Button
>

<style>
@layer components {
}
</style>
