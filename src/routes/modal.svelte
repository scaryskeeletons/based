<!-- Modal.svelte -->
<script>
  import { createEventDispatcher, onMount } from 'svelte';

  export let showModal = false;
  export let imageSrc = '';

  const dispatch = createEventDispatcher();

  function handleClickOutside(event) {
    if (event.target === event.currentTarget) {
      dispatch('close');
    }
  }

  // To ensure this works also when showModal changes without clicking
  onMount(() => {
    window.addEventListener('keydown', (event) => {
      if (event.key === 'Escape') {
        dispatch('close');
      }
    });
  });
</script>

{#if showModal}
<div class="modal-backdrop" on:click={handleClickOutside}>
  <div class="modal-content">
    <img src={imageSrc} alt="Enlarged image">
  </div>
</div>
{/if}

<style>
  @import "styles/styles.css";
</style>
