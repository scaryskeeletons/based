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

  function close() {
    dispatch('close');
  }

  // To ensure this works also when showModal changes without clicking
  onMount(() => {
    window.addEventListener('keydown', (event) => {
      if (event.key === 'Escape') {
        close();
      }
    });
  });
</script>

{#if showModal}
<div class="modal-backdrop" on:click={handleClickOutside}>
  <div class="modal-content">
    <button class="modal-close" on:click={close}>X</button>
    <img src={imageSrc} alt="Enlarged image">
  </div>
</div>
{/if}

<style>
  @import "../styles/styles.css";
  
  .modal-content {
    position: relative;
    padding: 20px; /* Ensure there's space for the close button */
  }

  .modal-close {
    z-index: 2001;
    position: fixed;
    top: 0;
    right: 0;
    border: none;
    background: transparent;
    color: #ff0202; /* Adjust based on your modal's styling */
    font-size: 40px;
    cursor: pointer;
    font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    padding: 5px 5px 5px 5px; /* Adjust for better positioning */
  }

  .modal-backdrop {
    position: fixed;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
