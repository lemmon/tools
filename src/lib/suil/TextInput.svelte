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
  before,
  after,
  header,
  footer,
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
  {before}
  {after}
  {header}
  {footer}
>
  {#snippet children({ id })}
    <input
      {id}
      class="suil-control"
      class:suil-control--stuck-left={before}
      class:suil-control--stuck-right={after || props.readonly}
      {...props}
      bind:value
    />
    {#if props.readonly}
      <div class="suil-field__icon">
        <EditOffIcon class="suil-icon" />
      </div>
    {/if}
  {/snippet}
</Field>

<style>
@layer components {
  .suil-control {
    appearance: textfield;
    display: block;
    background-color: transparent;
    color: inherit;
    margin: 0;
    padding: var(--suil-size);
    border: 0;
    width: 100%;
    font: var(--suil-font, inherit);
    outline: 0;
  }

  .suil-control::placeholder {
    color: color-mix(in oklch, currentColor 50%, transparent);
    opacity: 1;
  }

  .suil-control::-webkit-inner-spin-button,
  .suil-control::-webkit-outer-spin-button {
    appearance: none;
    margin: 0;
  }

  .suil-control--stuck-left {
    padding-left: 0;
  }

  .suil-control--stuck-right {
    padding-right: 0;
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
