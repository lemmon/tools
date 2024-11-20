<script>
// Global Stylesheet
import './styles.css';

// Local Dependencies
import Label from './Label.svelte';

//

let {
  id = `f_${crypto.randomUUID().replace(/\W/g, '')}`,
  class: classname,
  label,
  info,
  disabled,
  error,
  children,
  before,
  after,
  header,
  footer,
  ...props
} = $props();
</script>

<div
  class="suil-component suil-field {classname || ''}"
  {...props}
  data-error={!!error || null}
  data-disabled={disabled || null}
>
  {#if label}
    <Label for={id}
      >{#if typeof label === 'function'}{@render label()}{:else}{label}{/if}</Label
    >
  {/if}
  <div class="suil-field__control">
    {@render before?.()}
    {@render children({ id })}
    {@render after?.()}
  </div>
  {#if error && typeof error === 'string'}
    <div class="suil-component suil-field__footer">{error}</div>
  {:else if info}
    <div class="suil-component suil-field__footer">{info}</div>
  {/if}
  {@render footer?.()}
</div>

<style>
@layer components {
  .suil-component {
    font: var(--suil-font, inherit);
  }

  .suil-field {
    display: flex;
    flex-direction: column;
    gap: var(--suil-field-gap);
  }

  .suil-field__control {
    display: flex;
    flex-direction: row;
    position: relative;
    background-color: var(--suil-shade-100);
    color: inherit;
    margin: 0;
    padding: 0;
    border: 0;
    border-radius: var(--suil-border-radius, 0);
    outline: var(--suil-border-width) solid var(--suil-shade-400);
    outline-offset: calc(0px - var(--suil-border-width));
    overflow: clip;
  }

  /* Hover, Focus, Active */

  .suil-field:not([data-disabled]) .suil-field__control:focus-within {
    outline: var(--suil-focus-width) solid var(--suil-focus);
    outline-offset: calc(0px - var(--suil-focus-width));
    box-shadow: inset 0 0 0 calc(var(--suil-focus-width) + 1px) var(--suil-label);
  }

  /* Disabled */

  .suil-field[data-disabled] {
    color: var(--suil-shade-300);
    & .suil-field__control {
      outline-color: var(--suil-shade-300);
    }
  }

  /* Error State */

  .suil-field[data-error] .suil-field__control {
    outline-color: var(--suil-danger);
    background-color: color-mix(in srgb, var(--suil-shade-100), var(--suil-danger) 1%);
  }

  .suil-field[data-error] .suil-field__footer {
    color: var(--suil-danger);
  }
}
</style>
