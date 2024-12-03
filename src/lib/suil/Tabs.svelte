<script>
import { setContext } from 'svelte';

let { class: classname, value = $bindable(), children, ...props } = $props();

setContext('selected', {
  get value() {
    return value;
  },
  set value(newValue) {
    value = newValue;
  },
});
</script>

<div class="suil-component suil-tabs {classname || ''}" {...props}>
  {@render children()}
</div>

<style>
@layer components {
  .suil-tabs {
    display: flex;
    flex-direction: row;
    gap: 2px;
    background-color: var(--suil-shade-100);
    border-radius: var(--suil-border-radius, 0);
    outline: var(--suil-border-width) solid var(--suil-shade-200);
    outline-offset: calc(0px - var(--suil-border-width));
    padding: var(--suil-inset);
  }

  .suil-tabs :global(.suil-button) {
    padding: 0.5rem 1rem;
    border-radius: calc(var(--suil-border-radius, 0) - 2px);
  }

  .suil-tabs :global(.suil-button[data-kind='selected']) {
    background-color: var(--suil-background);
    color: var(--suil-color);
    outline: var(--suil-border-width) solid var(--suil-shade-300);
    outline-offset: calc(0px - var(--suil-border-width));
    & :global(.suil-button__label),
    & :global(.suil-button__loader) {
      color: currentColor;
    }
  }

  .suil-tabs :global(.suil-button[data-selected]) {
    background-color: var(--suil-background);
    outline: var(--suil-border-width) solid var(--suil-shade-300);
    outline-offset: calc(0px - var(--suil-border-width));
  }
}
</style>
