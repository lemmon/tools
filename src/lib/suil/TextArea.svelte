<script>
// Global Stylesheet
import './styles.css';

// Local Dependencies
import Field from './Field.svelte';

// Icons
import EditOffIcon from 'carbon-icons-svelte/lib/EditOff.svelte';

//

let {
  id,
  class: classname,
  style,
  value = $bindable(),
  label,
  counter = false,
  info,
  error,
  ...props
} = $props();
</script>

{#snippet labelBlock()}
  {label}
  {#if counter && props.maxlength}
    <span class="ml-auto">{value?.length || 0}/{props.maxlength}</span>
  {/if}
{/snippet}

<Field
  {id}
  class={classname}
  {style}
  disabled={props.disabled}
  label={label || (counter && props.maxlength) ? labelBlock : null}
  {info}
  {error}
>
  {#snippet children({ id })}
    <div
      class="suil-control"
      class:suil-control--stuck-left={false}
      class:suil-control--stuck-right={props.readonly}
    >
      <textarea class="suil-control__textarea" {id} {...props} bind:value></textarea>
      <div class="suil-control__preview">{value}_</div>
    </div>
    {#if props.readonly}
      <div class="suil-field__icon"><EditOffIcon class="suil-icon" /></div>
    {/if}
  {/snippet}
</Field>

<style>
@layer components {
  .suil-control {
    display: block;
    position: relative;
    width: 100%;
    min-height: calc(var(--suil-size) * 2 + 1lh * var(--suil-textarea-min-lines, 1));
  }

  .suil-control__textarea,
  .suil-control__preview {
    display: block;
    padding: var(--suil-size);
  }

  .suil-control__textarea {
    appearance: textfield;
    background-color: transparent;
    color: inherit;
    width: 100%;
    margin: 0;
    border: 0;
    outline: 0;
    font: var(--suil-font, inherit);
    position: absolute;
    inset: 0;
    resize: none;
  }

  .suil-control__preview {
    white-space: pre-wrap;
    overflow-wrap: break-word;
    word-break: normal;
    visibility: hidden;
  }

  .suil-control--stuck-left {
    & .suil-control__textarea,
    & .suil-control__preview {
      padding-left: 0;
    }
  }

  .suil-control--stuck-right {
    & .suil-control__textarea,
    & .suil-control__preview {
      padding-right: 0;
    }
  }

  .suil-field__icon {
    padding: calc(var(--suil-size));
    display: flex;
    justify-content: center;
    align-items: center;
    align-self: start;
  }

  /* Disabled */

  .suil-control:disabled {
    cursor: not-allowed;
  }
}
</style>
