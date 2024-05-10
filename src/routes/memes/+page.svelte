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
  
    const imageCount = 18;
    let images = Array.from({ length: imageCount }, (_, i) => `./s${i + 1}.avif`);
  </script>
  
  <div class="container">
      <div class="section" id="intro">
        <h1 class="rainbow-text spinning-text">Memes</h1>
        <p>$BASED full meme gallery</p>
        <div class="gallery">
            {#each images as image, i}
              <div class="image">
                <img src={image} alt={`Image ${i + 1}`} on:click={() => openModal(image)}>
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
  