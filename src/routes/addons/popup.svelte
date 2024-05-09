<script>
    import { onMount } from 'svelte';
  
    let show = true;
    let animate = false; // Controls the shaking animation
    let staticEffect = false; // Controls when to display static
  
    onMount(() => {
      setTimeout(() => {
        animate = true; // Start the shake
        setTimeout(() => {
          animate = false;
          staticEffect = true; // Enable static effect
          generateStatic();
          setTimeout(() => {
            show = false; // Hide the popup and stop the static effect
          }, 250); // Duration of the static effect before hiding
        }, 500); // Duration of the shake before static starts
      }, 3500); // Delay before the shake starts
    });
  
    // Function to generate static
    function generateStatic() {
      const canvas = document.getElementById('staticCanvas');
      const ctx = canvas.getContext('2d');
  
      function drawStatic() {
        const imageData = ctx.createImageData(canvas.width, canvas.height);
        for (let i = 0; i < imageData.data.length; i += 4) {
          const color = Math.random() * 255;
          imageData.data[i] = color;       // Red
          imageData.data[i + 1] = color;   // Green
          imageData.data[i + 2] = color;   // Blue
          imageData.data[i + 3] = 255;     // Alpha
        }
        ctx.putImageData(imageData, 0, 0);
        if (staticEffect) requestAnimationFrame(drawStatic);
      }
  
      drawStatic();
    }
  </script>
  
  {#if show}
    <div class:shake={animate} class:static={staticEffect} class="landing-popup">
      <canvas id="staticCanvas" width="window.innerWidth" height="window.innerHeight"
              style="position: fixed; top: 0; left: 0; width: 100%; height: 100%;"></canvas>
    </div>
  {/if}
  
  <style>
    .landing-popup {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-repeat: no-repeat;
      background-size: cover;
      background-image: url('https://github.com/scaryskeeletons/based/raw/main/static/notice_of_seizure.avif');
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      z-index: 10;
      overflow: hidden;
    }
    
    /* Shaking keyframes */
    @keyframes shake {
      0%, 100% { transform: translateX(0); }
      10%, 30%, 50%, 70%, 90% { transform: translateX(-10px); }
      20%, 40%, 60%, 80% { transform: translateX(10px); }
    }
    
    .shake {
      animation: shake 500ms; /* Animation duration matches the time to start hiding */
    }
  </style>
  