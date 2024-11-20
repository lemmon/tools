<script>
// Global Stylesheet
import './styles.css';

// Local Dependencies
import CopyButton from './CopyButton.svelte';

//

let { class: classname, code, copy = true } = $props();
</script>

<div class="suil-component suil-code {classname}">
  <pre><code>{code || ' '}</code></pre>
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

  .suil-code pre {
    flex: 1;
    padding: var(--suil-size);
    padding-right: 0;
    white-space: pre-wrap;
    word-break: normal;
    word-break: break-word; /* Safari */
    overflow-wrap: anywhere;
    font: var(--suil-code-font, inherit);
  }
}
</style>
