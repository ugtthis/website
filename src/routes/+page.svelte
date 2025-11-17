<script>
  import FourImage from "$lib/images/products/comma-four/four_screen_on_1.png";
  import DiamondGradient from "$lib/images/diamond-gradient-2.png";
  import MonumentExtendedBlack from "$lib/fonts/MonumentExtended/MonumentExtended-Black.woff2";
  import ExplodedSpecs from "$lib/images/exploded-specs-blur.png";
  import ExplodedSpecsMobile from "$lib/images/mobile-exploded-specs-blur.png";
  import CompatBrandsBanner from "$lib/images/compat-brands-banner.png";
  import DrivingCabinPov from "$lib/images/driving-cabin-pov.png";
  import GalleryFront from "$lib/images/products/comma-four/gallery/four_front.png";
  import GallerySide from "$lib/images/products/comma-four/gallery/four_side.png";
  import GalleryBack from "$lib/images/products/comma-four/gallery/four_back.png";
  import GalleryAngled from "$lib/images/products/comma-four/gallery/four_angled.png";
  import LightningIcon from "$lib/icons/ui/lightning-fast.svg?raw";
  import CalendarIcon from "$lib/icons/ui/calendar.svg?raw";
  import WifiIcon from "$lib/icons/ui/wifi.svg?raw";
  import MoneyIcon from "$lib/icons/ui/money.svg?raw";
  import CordIcon from "$lib/icons/ui/cord.svg?raw";

  const galleryImages = [
    { src: GalleryFront, alt: "comma four front" },
    { src: GallerySide, alt: "comma four side" },
    { src: GalleryBack, alt: "comma four back" },
    { src: GalleryAngled, alt: "comma four angled" }
  ];

  let selectedImage = galleryImages[0];

  function selectImage(image) {
    selectedImage = image;
  }
</script>

<svelte:head>
  <link
    rel="preload"
    href={MonumentExtendedBlack}
    as="font"
    type="font/woff2"
    crossorigin="anonymous"
  />
  <link rel="preload" as="image" href={DiamondGradient} />
  <link rel="preload" as="image" href={FourImage} />
</svelte:head>

<div class="page-wrapper">
<div class="hero-section">
  <div class="hero-container">
    <h1 class="hero-title">
      <span class="title-comma">COMMA</span><br>
      <span class="title-four">FOUR</span>
    </h1>

    <div class="center-content">
      <div class="gradient-device-wrapper">
        <img src={DiamondGradient} alt="" class="gradient-background" draggable="false" />
        <div class="device-container">
          <img src={FourImage} alt="comma four device" class="device-image" draggable="false" />
        </div>
      </div>
    </div>

    <div class="hero-buttons">
      <a href="/shop/comma-four" class="btn-buy-now">
        BUY NOW
      </a>
      <a href="#specs" class="btn-learn-more">
        Learn More
      </a>
    </div>
  </div>
</div>

<section class="banners-section banner-compat-brands">
  <div class="banner-container">
    <img src={CompatBrandsBanner} alt="Compatible car brands" class="banner-image" />
    <h2 class="banner-text">Works with over<br>325+ cars</h2>
  </div>
</section>

<section id="specs" class="specs-section">
  <div class="specs-container">
    <h2 class="specs-title">SPECS</h2>
    <div class="specs-image-wrapper">
      <img src={ExplodedSpecs} alt="Comma Four Exploded Specs" class="specs-image specs-image-desktop" />
      <img src={ExplodedSpecsMobile} alt="Comma Four Exploded Specs" class="specs-image specs-image-mobile" />
    </div>
  </div>
</section>

<section class="included-things-section">
  <div class="included-things-container">
    <h2 class="included-things-title">What's Included</h2>

    <div class="included-things-table">
      <div class="included-things-row">
        <span class="included-things-icon">{@html CordIcon}</span>
        <span class="included-things-item">Free car harness with purchase</span>
      </div>
      <div class="included-things-row">
        <span class="included-things-icon">{@html LightningIcon}</span>
        <span class="included-things-item">Instant cure device mounts</span>
      </div>
      <div class="included-things-row">
        <span class="included-things-icon">{@html CalendarIcon}</span>
        <span class="included-things-item">1-year limited warranty against hardware defects</span>
      </div>
      <div class="included-things-row">
        <span class="included-things-icon">{@html WifiIcon}</span>
        <span class="included-things-item">One free month of comma prime</span>
      </div>
      <div class="included-things-row">
        <span class="included-things-icon">{@html MoneyIcon}</span>
        <span class="included-things-item">30-day money-back trial</span>
      </div>
    </div>
  </div>
</section>

<section class="banners-section banner-driving">
  <div class="banner-container">
    <img src={DrivingCabinPov} alt="Driving cabin view" class="banner-image" />
    <h2 class="banner-text">make driving chill.</h2>
  </div>
</section>

<section class="gallery-section">
  <div class="gallery-container">
    <h2 class="gallery-title">GALLERY</h2>

    <div class="gallery-grid">
      <div class="gallery-main">
        <img src={selectedImage.src} alt={selectedImage.alt} class="gallery-main-image" />
      </div>

      <div class="gallery-thumbnails">
        {#each galleryImages as image}
          <button
            class="gallery-thumbnail"
            class:active={selectedImage === image}
            on:click={() => selectImage(image)}
            type="button"
          >
            <img src={image.src} alt={image.alt} class="gallery-thumb-image" />
          </button>
        {/each}
      </div>
    </div>

    <a href="/shop/comma-four" class="gallery-buy-button">
      Buy
    </a>
  </div>
</section>
</div>

<style>
  :global(html) {
    scroll-behavior: smooth;
  }

  .page-wrapper {
    position: relative;
    background-color: #D9D9D9;
    background-image: url("data:image/svg+xml,%3Csvg width='240' height='32' xmlns='http://www.w3.org/2000/svg'%3E%3Ctext x='8' y='18' font-family='monospace' font-size='11' fill='%23B0B0B0' opacity='0.25'%3E00101100 00110100 00101100 00110100 00101100 00110100%3C/text%3E%3Ctext x='8' y='32' font-family='monospace' font-size='11' fill='%23B0B0B0' opacity='0.25'%3E00110100 00101100 00110100 00101100 00110100 00101100%3C/text%3E%3C/svg%3E");
    background-size: 240px 32px;
    background-repeat: repeat;
    min-height: 100vh;
    padding-bottom: 4rem;

    @media screen and (max-width: 768px) {
      padding-bottom: 3rem;
    }
  }

  .page-wrapper::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 900px;
    background: linear-gradient(to bottom, rgba(0, 0, 0, 0.9) 0%, transparent 100%);
    pointer-events: none;
    z-index: 0;
  }

  @font-face {
    font-display: swap;
    font-family: "Monument Extended Black";
    font-style: normal;
    src: url("$lib/fonts/MonumentExtended/MonumentExtended-Black.woff2");
  }

  .hero-section {
    position: relative;
    width: 100%;
    display: flex;
    align-items: flex-start;
    justify-content: center;
    overflow: hidden;
    padding-top: 2rem;
    padding-bottom: 6rem;
    background: none;

    @media screen and (max-width: 768px) {
      padding-top: 1rem;
      padding-bottom: 2.5rem;
    }
  }

  .hero-container {
    position: relative;
    width: 100%;
    max-width: 1216px;
    display: flex;
    flex-direction: column;
    margin: 0 auto;
    z-index: 1;

    @media screen and (max-width: 768px) {
      padding: 1rem 1rem 0.5rem 1rem;
    }
  }

  .gradient-device-wrapper {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    max-width: 1200px;
  }

  .gradient-background {
    /* display: none; */
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 40%;
    min-width: 800px;
    height: auto;
    object-fit: contain;
    z-index: 0;
    user-select: none;
    pointer-events: none;

    @media screen and (max-width: 768px) {
      min-width: 600px;
    }

    @media screen and (max-width: 480px) {
      min-width: 500px;
    }
  }

  .hero-title {
    margin: 7rem auto 2rem auto;
    line-height: 0.55;
    font-family: "Monument Extended Black", sans-serif;
    font-size: clamp(40px, 7vw, 100px);
    font-weight: 900;
    letter-spacing: -0.02em;
    text-align: center;
    position: relative;
    z-index: 10;

    @media screen and (max-width: 768px) {
      margin: 6rem auto 2rem auto;
      font-size: clamp(60px, 10vw, 100px);
    }

    @media screen and (max-width: 480px) {
      margin: 7rem auto 1.5rem auto;
      font-size: clamp(50px, 12vw, 100px);
    }
  }

  .title-comma {
    color: #000000;
    display: block;
  }

  .title-four {
    margin-top: -0.15em;
    background: linear-gradient(180deg, #125a24 0%, #84ff00 100%);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    font-weight: 900;
  }

  .center-content {
    display: flex;
    justify-content: center;
    margin-bottom: 5rem;

    @media screen and (max-width: 768px) {
      margin-bottom: 2rem;
    }

    @media screen and (max-width: 480px) {
      margin-bottom: 1.5rem;
    }
  }

  .device-container {
    position: relative;
    max-width: 380px;

    @media screen and (max-width: 1200px) {
      max-width: 350px;
    }

    @media screen and (max-width: 768px) {
      max-width: 300px;
    }

    @media screen and (max-width: 480px) {
      max-width: 60vw;
    }
  }

  .device-image {
    width: 100%;
    height: auto;
    display: block;
    user-select: none;
    -webkit-user-drag: none;
    filter: drop-shadow(0 20px 40px rgba(0, 0, 0, 0.5));
  }

  .hero-buttons {
    position: relative;
    display: flex;
    flex-direction: row;
    gap: 1.5rem;
    align-self: center;
    width: 80%;
    max-width: 600px;
    padding-bottom: 1rem;
    z-index: 1;

    @media screen and (max-width: 768px) {
      flex-direction: column;
      align-items: center;
      gap: 1rem;
      padding-bottom: 0.5rem;
      width: 100%;
      max-width: 100%;
    }
  }

  .btn-buy-now {
    background: #000;
    color: #00FF40;
    font-family: "Monument Extended Black", sans-serif;
    font-size: 18px;
    letter-spacing: 0.5px;
    padding: 16px 30px;
    text-decoration: none;
    display: flex;
    align-items: center;
    justify-content: center;
    flex: 1;
    text-transform: uppercase;
    transition: all 0.2s ease;

    &:hover {
      transform: translateY(-2px);
    }

    &:active {
      transform: scale(0.98);
    }

    @media screen and (max-width: 768px) {
      width: 50%;
    }

    @media screen and (max-width: 480px) {
      font-size: 16px;
    }
  }

  .btn-learn-more {
    background: rgba(243, 243, 243, 0.432);
    color: #ffffff;
    font-family: 'JetBrains Mono', monospace;
    font-size: 18px;
    font-weight: 500;
    text-transform: uppercase;
    padding: 16px 30px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex: 1;
    border: 2px solid #ffffff;
    backdrop-filter: blur(1px);
    -webkit-backdrop-filter: blur(1px);
    transition: all 0.2s ease;

    &:hover {
      transform: translateY(-2px);
      background: rgba(255, 255, 255, 0.2);
    }

    &:active {
      transform: scale(0.98);
    }

    @media screen and (max-width: 768px) {
      width: 50%;
    }

    @media screen and (max-width: 480px) {
      font-size: 16px;
    }
  }

  .specs-section {
    width: 100%;
    padding: 4rem 0 6rem 0;
    background: none;

    @media screen and (max-width: 768px) {
      padding: 3rem 0 4rem 0;
    }
  }

  .specs-container {
    width: 80%;
    max-width: 1000px;
    margin: 0 auto;
    padding: 0 2rem;

    @media screen and (max-width: 768px) {
      width: 90%;
      padding: 0 1rem;
    }
  }

  .specs-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 3rem;
    font-weight: 700;
    color: #000;
    margin: 0 0 2rem 0;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    text-align: left;

    @media screen and (max-width: 768px) {
      font-size: 2rem;
      margin: 0 0 1.5rem 0;
    }
  }

  .specs-image-wrapper {
    width: 100%;
    display: flex;
    justify-content: flex-start;
    align-items: center;
  }

  .specs-image {
    width: 100%;
    height: auto;
    display: block;
  }

  .specs-image-mobile {
    display: none;
  }

  @media screen and (max-width: 850px) {
    .specs-image-desktop {
      display: none;
    }

    .specs-image-mobile {
      display: block;
    }
  }

  .banners-section {
    width: 100vw;
    position: relative;
    left: 50%;
    right: 50%;
    margin-left: -50vw;
    margin-right: -50vw;
    padding: 0;
    background: #000000;
    overflow: hidden;
  }

  .banner-compat-brands {
    height: 300px;

    @media screen and (max-width: 850px) {
      height: 220px;
    }

    @media screen and (max-width: 480px) {
      height: 150px;
    }
  }

  .banner-driving {
    height: 550px;

    @media screen and (max-width: 1200px) {
      height: 450px;
    }

    @media screen and (max-width: 980px) {
      height: 350px;
    }

    @media screen and (max-width: 768px) {
      height: 250px;
    }

    @media screen and (max-width: 480px) {
      height: 190px;
    }
  }

  .banner-container {
    position: relative;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  .banner-image {
    max-width: 100%;
    max-height: 100%;
    width: 100%;
    height: 100%;
    display: block;
    object-fit: contain;
  }

  .banner-text {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-family: Inter, sans-serif;
    font-size: clamp(2rem, 4vw, 3rem);
    font-weight: 600;
    color: #ffffff;
    text-align: center;
    margin: 0;
    padding: 0 .25rem;
    line-height: 1.2;
    white-space: nowrap;

    @media screen and (max-width: 480px) {
      font-size: clamp(1.5rem, 4vw, 2.25rem);
    }
  }

  .gallery-section {
    width: 100%;
    padding: 6rem 2rem 4rem 2rem;
    background: none;

    @media screen and (max-width: 768px) {
      padding: 4rem 1rem 3rem 1rem;
    }
  }

  .gallery-container {
    max-width: 1000px;
    margin: 0 auto;
    padding: 0 2rem;

    @media screen and (max-width: 768px) {
      padding: 0 1rem;
    }
  }

  .gallery-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 3rem;
    font-weight: 700;
    color: #000;
    margin: 0 0 2rem 0;
    text-transform: uppercase;
    letter-spacing: 0.05em;

    @media screen and (max-width: 768px) {
      font-size: 2rem;
      margin: 0 0 1.5rem 0;
    }
  }

  .gallery-grid {
    display: flex;
    gap: 0;
    margin-bottom: 3rem;
    max-width: 100%;

    @media screen and (max-width: 768px) {
      flex-direction: column;
      margin-bottom: 2rem;
    }
  }

  .gallery-main {
    flex: 1;
    max-width: 800px;
    aspect-ratio: 1;
    border: 2px solid #ffffff;
    background: rgba(243, 243, 243, 0.432);
    backdrop-filter: blur(1px);
    -webkit-backdrop-filter: blur(1px);
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .gallery-main-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .gallery-thumbnails {
    display: flex;
    flex-direction: column;
    gap: 0;

    @media screen and (max-width: 768px) {
      flex-direction: row;
      overflow-x: auto;
    }
  }

  .gallery-thumbnail {
    flex: 1;
    max-width: 200px;
    aspect-ratio: 1;
    border: 2px solid #ffffff;
    border-left: none;
    border-top: none;
    background: rgba(243, 243, 243, 0.432);
    backdrop-filter: blur(1px);
    -webkit-backdrop-filter: blur(1px);
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.2s ease;
    padding: 0;

    &:first-child {
      border-top: 2px solid #ffffff;
    }

    &:hover {
      opacity: 0.8;
    }

    &.active {
      background: rgba(243, 243, 243, 0.7);
      opacity: 1;
    }

    @media screen and (max-width: 768px) {
      flex: 1;
      width: 25%;
      height: auto;
      max-width: none;
      border-left: none;
      border-top: none;

      &:first-child {
        border-left: 2px solid #ffffff;
        border-top: none;
      }
    }
  }

  .gallery-thumb-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .gallery-buy-button {
    display: block;
    width: 100%;
    padding: 2rem;
    background: rgba(243, 243, 243, 0.432);
    backdrop-filter: blur(1px);
    -webkit-backdrop-filter: blur(1px);
    border: 2px solid #ffffff;
    font-family: Inter, sans-serif;
    font-size: 2rem;
    font-weight: 700;
    color: #000000;
    text-align: center;
    text-decoration: none;
    text-transform: capitalize;
    transition: all 0.2s ease;

    &:hover {
      background: rgba(243, 243, 243, 0.6);
    }

    @media screen and (max-width: 768px) {
      font-size: 1.5rem;
      padding: 1.5rem;
    }
  }

  .included-things-section {
    padding: 0 2rem 4rem 2rem;
    background: none;

    @media screen and (max-width: 768px) {
      padding: 0 1rem 3rem 1rem;
    }
  }

  .included-things-container {
    max-width: 1000px;
    margin: 0 auto;
    padding: 0 2rem;

    @media screen and (max-width: 768px) {
      padding: 0 1rem;
    }
  }

  .included-things-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 2rem;
    font-weight: 700;
    color: #000;
    margin: 0 0 2rem;
    text-transform: uppercase;

    @media screen and (max-width: 768px) {
      font-size: 1.5rem;
      margin: 0 0 1.5rem;
    }
  }

  .included-things-table {
    display: flex;
    flex-direction: column;
  }

  .included-things-row {
    background: rgba(243, 243, 243, 0.2);
    backdrop-filter: blur(1px);
    -webkit-backdrop-filter: blur(1px);
    border: 2px solid #ffffff;
    border-top: none;
    padding: 1.75rem 2rem;
    display: flex;
    align-items: center;
    gap: 1.5rem;

    &:first-child {
      border-top: 2px solid #ffffff;
    }

    @media screen and (max-width: 768px) {
      padding: 1.5rem 1.5rem;
    }
  }

  .included-things-icon {
    flex-shrink: 0;
    width: 32px;
    height: 32px;

    @media screen and (max-width: 768px) {
      width: 28px;
      height: 28px;
    }
  }

  .included-things-item {
    font-family: 'JetBrains Mono', monospace;
    font-size: 1.25rem;
    font-weight: 300;
    color: #000;

    @media screen and (max-width: 850px) {
      font-size: 1rem;
    }

    @media screen and (max-width: 480px) {
      font-size: 0.75rem;
    }
  }
</style>
