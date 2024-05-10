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
  
    // Timeout to delay the loading of sections
    setTimeout(() => {
      sectionsVisible = true;
    }, 1000); // Delay of 1000 milliseconds (1 second)
  
    const imageCount = 12;
    const normieCount = 24;
    let images = Array.from({ length: imageCount }, (_, i) => `./s${i + 1}.avif`);
  </script>
  
  <div class="container">
    {#if sectionsVisible}
  
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
      {/if}
  </div>
  
  <Modal {showModal} imageSrc={selectedImage} on:close={closeModal}/>
  
  <style>
    @import "../styles/styles.css";
  </style>
  