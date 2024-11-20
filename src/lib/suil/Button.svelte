<script>
// Global Stylesheet
import './styles.css';

// Local Dependencies
import Loader from './Loader.svelte';

//

let { href, class: classname, kind, disabled, loading = false, children, ...props } = $props();
</script>

{#if !href || disabled || loading}
  <button
    disabled={disabled || loading}
    class="suil-component suil-button {classname || ''}"
    data-kind={kind}
    data-loading={loading || null}
    {...props}
  >
    <span class="suil-button__label">{@render children()}</span>
    {#if loading}
      <span class="suil-button__loader"><Loader /></span>
    {/if}
  </button>
{:else}
  <a {href} class="suil-component suil-button {classname || ''}" data-kind={kind} {...props}>
    <span class="suil-button__label">{@render children()}</span>
  </a>
{/if}

<style>
@layer components {
  .suil-button {
    --suil-emphasis-100: color-mix(in srgb, currentColor, var(--suil-emphasis) 10%);
    --suil-emphasis-200: color-mix(in srgb, currentColor, var(--suil-emphasis) 20%);
    appearance: none;
    display: block;
    position: relative;
    margin: 0;
    padding: var(--suil-size);
    border: none;
    border-radius: var(--suil-border-radius, 0);
    overflow: clip;
    width: initial;
    font: var(--suil-font);
    background-color: currentColor;
    color: var(--suil-color);
    transition: initial;
    cursor: pointer;
    outline: 0;
  }

  .suil-button__label {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    gap: var(--suil-button-gap, 0);
    margin: 0 var(--suil-gutter, 0);
    color: var(--suil-label);
  }

  /* Hover, Focus, Active */

  .suil-button:not(:disabled):hover {
    background-color: var(--suil-emphasis-100);
  }

  .suil-button:not(:disabled):focus {
    outline: var(--suil-focus-width) solid var(--suil-focus);
    outline-offset: calc(0px - var(--suil-focus-width));
    box-shadow: inset 0 0 0 calc(var(--suil-focus-width) + 1px) var(--suil-background);
  }

  .suil-button:not(:disabled):active {
    background-color: var(--suil-emphasis-200);
  }

  /* Disabled */

  .suil-button:not([data-loading]):disabled {
    color: var(--suil-shade-400);
    background-color: var(--suil-shade-300);
    cursor: not-allowed;
    & .suil-button__label {
      color: currentColor;
      opacity: 0.4;
    }
  }

  /* Loading State */

  .suil-button__loader {
    position: absolute;
    inset: 0;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    color: var(--suil-label);
  }

  .suil-button[data-loading] {
    cursor: progress;
    & .suil-button__label {
      visibility: hidden;
    }
  }

  /* Kind = Outlined */

  .suil-button[data-kind='outlined'] {
    &:not(:hover, :focus, :active),
    &:disabled {
      background-color: transparent;
      outline: var(--suil-border-width) solid currentColor;
      outline-offset: calc(0px - var(--suil-border-width));
      & .suil-button__label,
      & .suil-button__loader {
        color: currentColor;
      }
    }
  }

  /* Kind = Ghost */

  .suil-button[data-kind='ghost'] {
    --suil-emphasis-100: color-mix(in srgb, transparent, var(--suil-shade-400) 10%);
    --suil-emphasis-200: color-mix(in srgb, transparent, var(--suil-shade-400) 20%);
    background-color: transparent;
    & .suil-button__label,
    & .suil-button__loader {
      color: currentColor;
    }
  }
}
</style>
