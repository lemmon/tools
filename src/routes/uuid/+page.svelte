<script>
import * as uuid from 'uuid';

let out = $state(null);

$effect(() => {
  generate();
});

function generate() {
  out = uuid.v4();
}
</script>

<div class="m-auto flex flex-col items-center gap-4 p-4">
  <h1>UUID v4</h1>
  <div class="flex flex-row items-center gap-4">
    {#if out}
      <h2 class="text-3xl leading-10">{out}</h2>
      <button
        class="bg-slate-200 p-3 active:bg-slate-300"
        type="button"
        onclick={() => {
          navigator.clipboard.writeText(out);
        }}>Copy</button
      >
    {:else}
      <div class="skeleton text-3xl leading-10">Loading&hellip;</div>
    {/if}
  </div>
  <div>
    <button class="bg-slate-900 p-4 text-white active:bg-slate-800" type="button" onclick={generate}
      >Generate new</button
    >
  </div>
</div>

<style>
.skeleton {
  position: relative;
  width: 32ch;
  color: transparent;
  background-color: var(--color-slate-200);
  &::before {
    content: '';
    display: block;
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    background-color: var(--color-slate-300);
    animation: 3s ease-in-out skeleton infinite;
  }
}

@keyframes skeleton {
  0% {
    opacity: 0.3;
    transform: scaleX(0);
    transform-origin: left;
  }
  20% {
    opacity: 1;
    transform: scaleX(1);
    transform-origin: left;
  }
  28% {
    transform: scaleX(1);
    transform-origin: right;
  }
  51% {
    transform: scaleX(0);
    transform-origin: right;
  }
  58% {
    transform: scaleX(0);
    transform-origin: right;
  }
  82% {
    transform: scaleX(1);
    transform-origin: right;
  }
  83% {
    transform: scaleX(1);
    transform-origin: left;
  }
  96% {
    transform: scaleX(0);
    transform-origin: left;
  }
  to {
    opacity: 0.3;
    transform: scaleX(0);
    transform-origin: left;
  }
}
</style>
