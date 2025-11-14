<script>
  import FourImage from "$lib/images/products/comma-four/four_screen_on.png";
  import DiamondGradient from "$lib/images/diamand-gradient.png";
  import MonumentExtendedBlack from "$lib/fonts/MonumentExtended/MonumentExtended-Black.woff2";
  import CartIcon from "$lib/icons/cart-2.svg?raw";
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
  <style>
    body {
      background-color: #D9D9D9;
    }
  </style>
</svelte:head>

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
        <span class="cart-icon">{@html CartIcon}</span>
      </a>
    <a href="/" class="btn-learn-more">
      Learn More
      <svg width="18" height="18" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg" class="chevron-icon">
        <path d="M4 6L8 10L12 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </a>
  </div>
  </div>
</div>

<style>
  @font-face {
    font-display: swap;
    font-family: "Monument Extended Black";
    font-style: normal;
    src: url("$lib/fonts/MonumentExtended/MonumentExtended-Black.woff2");
  }

  .hero-section {
    position: relative;
    min-height: 100vh;
    width: 100%;
    background: #D9D9D9;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  .hero-container {
    position: relative;
    width: 100%;
    max-width: 1216px;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    padding: 2rem;

    @media screen and (max-width: 768px) {
      padding: 1rem;
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
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 100%;
    min-width: 800px;
    height: auto;
    object-fit: contain;
    z-index: 0;
    user-select: none;
    pointer-events: none;
    mix-blend-mode: difference;

    @media screen and (max-width: 768px) {
      min-width: 600px;
    }

    @media screen and (max-width: 480px) {
      min-width: 500px;
    }
  }

  .hero-title {
    margin: 7rem 0 2rem 2rem;
    line-height: 0.55;
    font-family: "Monument Extended Black", sans-serif;
    font-size: clamp(40px, 7vw, 100px);
    font-weight: 900;
    letter-spacing: -0.02em;

    @media screen and (max-width: 768px) {
      margin: 6rem 0 2rem 1rem;
    }

    @media screen and (max-width: 480px) {
      margin: 7rem 0 1.5rem 0.5rem;
    }
  }

  .title-comma {
    color: #000000;
    display: block;
  }

  .title-four {
    margin-top: -0.15em;
    background: linear-gradient(180deg, #426f4d 0%, #84ff00 100%);
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
      margin-bottom: 4rem;
    }

    @media screen and (max-width: 480px) {
      margin-bottom: 3rem;
    }
  }

  .device-container {
    position: relative;
    max-width: 470px;

    @media screen and (max-width: 1200px) {
      max-width: 420px;
    }

    @media screen and (max-width: 768px) {
      max-width: 360px;
    }

    @media screen and (max-width: 480px) {
      max-width: 70vw;
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
    width: 100%;
    max-width: 600px;
    padding-bottom: 2rem;
    z-index: 1;

    @media screen and (max-width: 768px) {
      flex-direction: column;
      align-items: center;
      gap: 1rem;
      padding-bottom: 1rem;
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
    justify-content: space-between;
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

  .cart-icon {
    width: 18px;
    height: 18px;
    flex-shrink: 0;
    display: flex;
    align-items: center;

    & :global(svg) {
      display: block;
      width: 100%;
      height: 100%;
    }
  }

  .btn-learn-more {
    background: #8686863e;
    color: #ffffff;
    font-family: Inter, sans-serif;
    font-size: 18px;
    font-weight: 500;
    padding: 16px 30px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex: 1;
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

  .chevron-icon {
    flex-shrink: 0;
  }
</style>
