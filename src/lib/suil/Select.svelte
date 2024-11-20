<script>
// Global Stylesheet
import './styles.css';

// Local Dependencies
import Field from './Field.svelte';

// Icons
import ChevronSortIcon from 'carbon-icons-svelte/lib/ChevronSort.svelte';

//

let {
  id,
  class: classname,
  style,
  value = $bindable(),
  label,
  info,
  error,
  children,
  ...props
} = $props();
</script>

{#snippet control({ id })}
  <select {id} class="suil-control" {...props} bind:value>
    {@render children()}
  </select>
  <div class="suil-field__handle suil-field__icon"><ChevronSortIcon class="suil-icon" /></div>
{/snippet}

<Field
  {id}
  class={classname}
  {style}
  disabled={props.disabled}
  {label}
  {info}
  {error}
  children={control}
/>

<style>
@layer components {
  .suil-control {
    appearance: none;
    display: block;
    position: relative;
    z-index: 2;
    background-color: transparent;
    color: inherit;
    margin: 0;
    padding: var(--suil-size);
    padding-right: calc(var(--suil-size) * 2 + 1lh);
    border: 0;
    width: 100%;
    font: var(--suil-font, inherit);
    outline: 0;
  }

  .suil-field__handle {
    position: absolute;
    right: 0;
    top: 0;
    bottom: 0;
    z-index: 1;
  }

  .suil-field__icon {
    padding: calc(var(--suil-size));
    display: flex;
    justify-content: center;
    align-items: center;
  }

  /* Disabled */

  .suil-control:disabled {
    cursor: not-allowed;
  }
}
</style>
