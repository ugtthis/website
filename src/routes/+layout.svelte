<script>
  import "../app.css";

  import MonumentExtendedBlack from "$lib/fonts/MonumentExtended/MonumentExtended-Black.woff2";
  import "@fontsource/inter/400.css";
  import "@fontsource/inter/600.css";
  import "@fontsource/inter/700.css";
  import '@fontsource/jetbrains-mono/400.css';

  import { get } from "svelte/store";


  import { updateCart } from '$lib/utils/shopify';
  import { printConsoleBanner } from '$lib/utils/console';

  import CommandPalette from "$lib/components/CommandPalette.svelte";
  import ShoppingCart from "$lib/components/ShoppingCart.svelte";
  import CartNotification from "$lib/components/CartNotification.svelte";
  import {
    loadCart,
    cartId,
    cartTotalQuantity,
    showCart,
  } from "../store.js";

  import { onMount } from "svelte";

  let loading = false;

  async function openCart() {
    await loadCart();
    showCart.set(true);
  }

  function closeCart() {
    showCart.set(false);
  }

  async function toggleCart() {
    if ($showCart) {
      closeCart();
    } else {
      await openCart();
    }
  }

  async function updateProduct(event) {
    await updateCart({
      cartId: get(cartId),
      lineId: event.detail.body.lineId,
      quantity: event.detail.body.quantity,
      variantId: event.detail.body.variantId,
    });
    await loadCart();
    loading = false;
  }

  onMount(async () => {
    await loadCart();
    document.addEventListener("keydown", (e) => {
      if (e.key === "Escape") {
        closeCart();
      }
    });
  });

  printConsoleBanner();
</script>

<svelte:head>
  <link
    rel="preload"
    href={MonumentExtendedBlack}
    as="font"
    type="font/woff2"
    crossorigin="anonymous"
  />
</svelte:head>

<header class="navbar">
  <div class="navbar-container">
    <CommandPalette />
    {#if $cartTotalQuantity > 0}
      <CartNotification on:click={toggleCart} />
    {/if}
  </div>
</header>

{#if $showCart}
  <ShoppingCart
    on:click={closeCart}
    on:updateProduct={updateProduct}
    bind:loading
  />
{/if}

<main>
  <slot></slot>
</main>

<footer>
  <div class="footer-content">
    <div class="footer-left">
      <h1>COMMA</h1>
      <div class="copyright">© comma_ai 2025</div>
    </div>
    <div class="footer-right">
      <div class="footer-links-grid">
        <a href="https://connect.comma.ai">CONNECT</a>
        <a href="https://github.com/commaai/openpilot/releases">RELEASES</a>
        <a href="/jobs">JOBS</a>
        <a href="/leaderboard.html">LEADERBOARD</a>
        <a href="/vehicles">SUPPORTED CARS</a>
        <a href="/support">SUPPORT</a>
        <a href="/setup">SETUP GUIDE</a>
        <a href="https://github.com/commaai">GITHUB</a>
        <a href="https://twitter.com/comma_ai">TWITTER</a>
        <a href="https://www.instagram.com/comma_ai">INSTAGRAM</a>
        <a href="https://discord.comma.ai">DISCORD</a>
        <a href="https://www.youtube.com/commaai">YOUTUBE</a>
        <a href="/terms">TERMS & PRIVACY</a>
      </div>
    </div>
  </div>
</footer>

<style>
  @font-face {
    font-display: block;
    font-family: "Monument Extended Black";
    font-style: normal;
    src: url("$lib/fonts/MonumentExtended/MonumentExtended-Black.woff2");
  }

  .navbar {
    top: 1rem;
    position: fixed;
    left: 0;
    right: 0;
    width: 100%;
    z-index: 1000;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    pointer-events: none;
  }

  .navbar-container {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 8px;
    pointer-events: auto;
  }

  @media (max-width: 500px) {
    .navbar-container {
      width: 100%;
    }
  }


  footer {
    background-color: #333;
    padding: 0;
    margin: 0;
    position: relative;
    z-index: 10;
    border-top: 1px solid black;

    & .footer-content {
      background-color: #EAEAEA;
      padding: 1rem;
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      width: 100%;
      box-sizing: border-box;
      overflow-x: auto;
    }

    & .footer-left {
      display: flex;
      flex-direction: row;
      align-items: baseline;
      gap: 2rem;
    }

    & h1 {
      color: #000;
      font-family: "Monument Extended Black", sans-serif;
      font-size: 64px;
      text-transform: uppercase;
      margin: 0;
      padding: 0;
      line-height: 1;
    }

    & .footer-left .copyright {
      color: black;
      font-size: 0.875rem;
      margin: 0;
      padding: 0;
      font-family: 'JetBrains Mono', monospace;
      font-weight: 400;
      line-height: 1;
    }

    & .footer-right {
      display: flex;
      align-items: center;
      align-self: center;
    }

    & .footer-links-grid {
      display: grid;
      grid-template-columns: repeat(6, auto);
      gap: 0.75rem 60px;
      justify-content: flex-end;
      justify-items: end;
      grid-auto-flow: row;
      direction: rtl;

      @media screen and (max-width: 1440px) {
        grid-template-columns: repeat(4, auto);
      }

      @media screen and (max-width: 1170px) {
        grid-template-columns: repeat(3, auto);
      }

      @media screen and (max-width: 471px) {
        grid-template-columns: repeat(2, auto);
      }

      @media screen and (max-width: 300px) {
        grid-template-columns: repeat(1, auto);
      }
    }

    & .footer-links-grid a {
      direction: ltr;
      color: #000;
      text-transform: uppercase;
      font-size: 14px;
      font-weight: 400;
      text-decoration: none;
      font-family: 'JetBrains Mono', monospace;
      letter-spacing: 0.5px;
      transition: opacity 0.2s;
      line-height: 1;
      text-align: right;
      justify-self: end;
      align-self: end;
      width: 100%;
      display: block;
    }

    & .footer-links-grid a:hover,
    & .footer-links-grid a:active {
      opacity: 0.6;
    }

    /*@media screen and (max-width: 1024px) {*/
    /*  & .footer-content {*/
    /*    padding: 1rem;*/
    /*    flex-direction: column;*/
    /*    gap: 2rem;*/
    /*  }*/

    /*  & .footer-right {*/
    /*    align-items: flex-start;*/
    /*    width: 100%;*/
    /*  }*/

    /*  & .footer-links-grid {*/
    /*    grid-template-columns: repeat(auto-fit, minmax(120px, auto));*/
    /*    justify-content: flex-start;*/
    /*    width: 100%;*/
    /*    gap: 1.5rem 1.5rem;*/
    /*  }*/
    /*}*/

    @media screen and (max-width: 1010px) {
      & .footer-content {
        flex-direction: column;
        align-items: start;
        gap: 2rem;
      }

      & .footer-left {
        order: 2;
      }

      & .footer-right {
        order: 1;
        align-self: flex-start;
      }

      & .footer-links-grid {
        gap: 1rem 60px;
        justify-content: flex-start;
        justify-items: start;
        direction: ltr;
      }

      & .footer-links-grid a {
        text-align: left;
        justify-self: start;
      }
    }

    @media screen and (max-width: 500px) {
      & .footer-left {
        flex-direction: column;
        gap: 1rem;
      }
    }

    @media screen and (max-width: 698px) {
      & h1 {
        font-size: 48px;
      }
    }

  }
</style>
