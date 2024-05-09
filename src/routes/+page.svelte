<script>
  import Modal from './addons/modal.svelte';
  import LandingPopup from './addons/popup.svelte';
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
  let normies = Array.from({ length: normieCount }, (_, i) => `./normie${i + 1}.avif`);
  let textPlaceholders = Array.from({ length: normieCount }, (_, i) => `Normie ${i + 1}`);
</script>

<LandingPopup />

<div class="container">
  {#if sectionsVisible}
    <div class="section" id="intro">
      <h1 class="rainbow-text spinning-text">Welcome to $BASED</h1>
      <p>From Bank of America full-stack developer to $BASED founder.</p>
      <p>Dev is doxxed and here for the ride.</p>
    </div>

    <div class="section" id="links">
      <h1>$BASED Links</h1>
      <a href="https://t.me/DevBasedSolana" target="_blank">
        <button type="button">Telegram</button>
      </a>
      <a href="https://twitter.com/DevBasedSolana" target="_blank">
        <button type="button">Twitter</button>
      </a>
      <a href="https://www.dextools.io/app/en/solana/pair-explorer/7rhUbTbunhohLoxQs1powsr7hs4jKJVbuwgb3erzZ6HH?t=1715043598473" target="_blank">
        <button type="button">Dextools</button>
      </a>
      <a href="https://dexscreener.com/solana/7rhubtbunhohloxqs1powsr7hs4jkjvbuwgb3erzz6hh" target="_blank">
        <button type="button">Dexscreener</button>
      </a>
      <button type="button">Merch (TBA)</button>
    </div>

    <div class="section" id="about">
      <h2>About Anatoliy (The Dev)</h2>
      <p>Anatoliy's mission is to garner a large community and travel the world. The way he sees it is that with the power of his community he will grow the entire web3 ecosystem.</p>
      <img src='anatoliy.avif' alt={`Picture of Anatoliy`} on:click={() => openModal('anatoliy.avif')}>
    </div>

    <div class="section" id="gallery1">
      <h2 class="rainbow-text">FUCK THE BANKS</h2>
      <div class="gallery">
        {#each images as image, i}
          <div class="image">
            <img src={image} alt={`Image ${i + 1}`} on:click={() => openModal(image)}>
          </div>
        {/each}
      </div>
    </div>

    <div class="section" id="story">
      <h2>The Story</h2>
      <p>The Dev recently got TERMINATED from Bank of America for creating Fuck The Bank token. Many people made some good money, but the dev didn't sell at all. The dev is not a bitch and will never dump on friends/holders. $BASED wants to change the game in meme creating and set the standard high for any future devs. The dev is now full time into crypto and will continue working hard for your bag. The dev won't ever sell any tokens, only burn or give away.</p>
      <p>The goal is to get a Kick Contract and stream 24/7. $BASED wants to connect with Phantom Wallet and get a sponsorship. </p>
    </div>

    <div class="section" id="gallery2">
      <h2>Normies Onboarded</h2>
      <p>The dev has been traveling the world for the past 3 weeks onboarding normal everyday people into crypto using Phantom wallet and Dev $BASED on Solana.</p>
      <div class="gallery">
        {#each normies as image, i}
          <div class="image">
            <img src={image} alt={`Second Gallery Image ${i + 1}`} on:click={() => openModal(image)}>
            <p>{textPlaceholders[i]}</p>
          </div>
        {/each}
      </div>
    </div>

    <section class="contact-section">
      <div class="contact-intro">
        <h2 class="contact-title">Get in Touch</h2>
        <p class="contact-description">
          Fill out the form below and we'll get back to you as soon as possible.
        </p>
      </div>
      <form class="contact-form" action="https://api.web3forms.com/submit" method="POST">
        <input type="hidden" name="access_key" value="d0c0818b-c515-4cce-aee4-0cb7f7016dde" />
        <input type="hidden" name="redirect" value="https://devbasedsolana.com/">
        <input type="hidden" name="subject" value="New Contact Form Submission from Contact input" />
        <input type="hidden" name="from_name" value="BasedDev" />
        <div class="form-group-container">
          <div class="form-group">
            <label for="name" class="form-label">Name</label>
            <input id="name" name="name" class="form-input" placeholder="Your name" type="text" />
          </div>
          <div class="form-group">
            <label for="email" class="form-label">Email</label>
            <input id="email" name="email" class="form-input" placeholder="Your email" type="email" />
          </div>
          <div class="form-group">
            <label for="phone" class="form-label">Twitter</label>
            <input id="phone" name="phone" class="form-input" placeholder="Your twitter handle" type="text" />
          </div>
          <div class="form-group">
            <label for="message" class="form-label">Message</label>
            <textarea class="form-textarea" id="message" name="message" placeholder="Your message"></textarea>
          </div>
        </div>
        <button class="form-submit" type="submit">Send Message</button>
      </form>
    </section>
    {/if}
</div>

<Modal {showModal} imageSrc={selectedImage} on:close={closeModal}/>

<style>
  @import "./styles/styles.css";
</style>
