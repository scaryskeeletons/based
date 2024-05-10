<script>
    import Modal from '../addons/modal.svelte';
    let showModal = false;
    let selectedImage = '';
    let sectionsVisible = false;
  
    function openModal(imageSrc) {
      selectedImage = imageSrc;
      showModal = true;
    }
  
    function closeModal() {
      showModal = false;
    }
    const normieCount = 24;
    let normies = Array.from({ length: normieCount }, (_, i) => `./normie${i + 1}.avif`);
    let textPlaceholders = Array.from({ length: normieCount }, (_, i) => `Normie ${i + 1}`);
  </script>
  
  <div class="container">
      <div class="section" id="intro">
        <h1 class="rainbow-text spinning-text">NORMIES</h1>
        <p>$BASED full normie gallery</p>
        <div class="gallery">
            {#each normies as image, i}
              <div class="image">
                <img src={image} alt={`Second Gallery Image ${i + 1}`} on:click={() => openModal(image)}>
                <p>{textPlaceholders[i]}</p>
              </div>
            {/each}
          </div>
          <a href="/">
            <button type="button">Home</button>
          </a>
      </div>
  </div>
  
  <Modal {showModal} imageSrc={selectedImage} on:close={closeModal}/>
  
  <style>
    @import "../styles/styles.css";
  </style>
  