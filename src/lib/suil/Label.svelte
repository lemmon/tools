<script>
// Global Stylesheet
import './styles.css'

//

let { class: classname, children, ...props } = $props()
</script>

<label class="suil-component suil-label {classname || ''}" {...props}>{@render children()}</label>

<style>
@layer components {
  .suil-label {
    display: flex;
    flex-direction: row;
    font: var(--suil-font, inherit);
    color: var(--suil-label-color, currentColor);
  }
}
</style>
