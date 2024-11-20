<script>
// Global Stylesheet
import './styles.css'

// Local Dependencies
import Button from './Button.svelte'

// Icons
import CopyIcon from 'carbon-icons-svelte/lib/Copy.svelte'
import CheckmarkIcon from 'carbon-icons-svelte/lib/Checkmark.svelte'

//

let { text, onclick, ...props } = $props()

let copied = $state(null)

function handleCopy() {
  // perform copy
  clearInterval(copied)
  navigator.clipboard.writeText(text).then(() => {
    copied = setTimeout(() => {
      copied = null
    }, 1000)
  })

  // call onclick if present
  if (onclick) onclick()
}
</script>

<Button {...props} onclick={handleCopy}
  >{#if !copied}<CopyIcon class="suil-icon" />{:else}<CheckmarkIcon
      class="suil-icon"
    />{/if}</Button
>
