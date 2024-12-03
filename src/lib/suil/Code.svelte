<script>
// Global Stylesheet
import './styles.css';

// Local Dependencies
import CopyButton from './CopyButton.svelte';

//

let { class: classname, code, placeholder, copy = true } = $props();
</script>

<div class="suil-component suil-code {classname}">
  {#if code}
    <pre class="suil-code__code"><code>{code}</code></pre>
  {:else}
    <div class="suil-code__placeholder">{placeholder || ' '}</div>
  {/if}
  {#if copy}
    <div><CopyButton class="suil-button-inset" kind="ghost" text={code} /></div>
  {/if}
</div>

<style>
@layer components {
  .suil-code {
    display: flex;
    flex-direction: row;
    width: 100%;
    margin: 0;
    padding: 0;
    border: 0;
    border-radius: var(--suil-border-radius, 0);
    font: var(--suil-font, inherit);
    background-color: var(--suil-shade-100);
  }

  .suil-code__code,
  .suil-code__placeholder {
    flex: 1;
    padding: var(--suil-size);
    padding-right: 0;
  }

  .suil-code__code {
    white-space: pre-wrap;
    word-break: normal;
    word-break: break-word; /* Safari */
    overflow-wrap: anywhere;
    font: var(--suil-code-font, inherit);
  }

  .suil-code__code code {
    display: block;
  }

  .suil-code__placeholder {
    color: color-mix(in oklch, currentColor 50%, transparent);
  }
}
</style>
