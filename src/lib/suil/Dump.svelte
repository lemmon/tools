<script>
// Global Stylesheet
import './styles.css';

// Local Dependencies
import Code from './Code.svelte';

//

let { data, ...props } = $props();
</script>

<Code {...props} code={JSON.stringify(data, null, '  ')} />
