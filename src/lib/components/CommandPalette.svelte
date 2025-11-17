<script>
  import { onDestroy } from 'svelte';
  import { browser } from '$app/environment';
  import { goto } from '$app/navigation';
  import { page } from '$app/stores';
  import { clickOutside } from '$lib/utils/clickOutside';

  import CommaIcon from '$lib/icons/comma.svg?raw';
  import CmdKIcon from '$lib/icons/ui/cmd-k.svg?raw';
  import SteeringWheelIcon from '$lib/icons/ui/steering-wheel.svg?raw';
  import CartIcon from '$lib/icons/ui/cart-2.svg?raw';
  import TextBlogIcon from '$lib/icons/ui/text-blog.svg?raw';
  import NewWindowIcon from '$lib/icons/ui/new-window.svg?raw';
  import LightningBoltIcon from '$lib/icons/ui/lightning-bolt.svg?raw';
  import SupportQuestionIcon from '$lib/icons/ui/support-question.svg?raw';

  const navItems = [
    { label: 'HOME', href: '/', icon: SteeringWheelIcon },
    { label: 'SHOP', href: '/shop', icon: CartIcon },
    { label: 'BLOG', href: 'https://blog.comma.ai', icon: TextBlogIcon, external: true },
    { label: 'OPENPILOT', href: 'https://github.com/commaai/openpilot', icon: NewWindowIcon, external: true },
    { label: 'JOBS', href: '/jobs', icon: LightningBoltIcon },
    { label: 'FAQ', href: '/support', icon: SupportQuestionIcon }
  ];

  let isOpen = false;
  let searchInput = '';
  let selectedIndex = 0;
  let searchInputElement;
  let paletteElement;
  let isUsingKeyboard = false;

  function findCurrentPageItem(pathname) {
    return navItems.reduce((best, item) => {
      if (item.external) return best;

      const isMatch = item.href === '/'
        ? pathname === '/'
        : pathname === item.href || pathname.startsWith(item.href + '/');

      if (isMatch && (!best || item.href.length > best.href.length)) {
        return item;
      }
      return best;
    }, null);
  }

  $: filteredItems = navItems.filter(item =>
    item.label.toLowerCase().startsWith(searchInput.toLowerCase())
  );

  $: currentPageItem = findCurrentPageItem($page.url.pathname);
  $: currentPageIndex = currentPageItem ? filteredItems.indexOf(currentPageItem) : -1;

  $: if (filteredItems.length > 0 && selectedIndex >= filteredItems.length) {
    selectedIndex = 0;
  }

  $: if (browser && isOpen) {
    const isMobile = window.matchMedia('(max-width: 500px)').matches;
    if (isMobile) {
      document.body.style.overflow = 'hidden';
    }
  } else if (browser) {
    document.body.style.overflow = '';
  }

  function navigateToItem(item) {
    if (item.external) {
      window.open(item.href, '_blank');
    } else {
      goto(item.href);
    }
    closePalette();
  }

  function togglePalette() {
    if (isOpen) {
      closePalette();
    } else {
      isOpen = true;
      selectedIndex = Math.max(0, currentPageIndex);
      searchInput = '';
      isUsingKeyboard = false;
      if (browser) {
        const isMobile = window.matchMedia('(max-width: 500px)').matches;
        if (!isMobile) {
          setTimeout(() => searchInputElement?.focus(), 0);
        }
      }
    }
  }

  function closePalette() {
    isOpen = false;
    searchInput = '';
    selectedIndex = 0;
    isUsingKeyboard = false;
  }

  function handleGlobalKeydown(event) {
    if ((event.metaKey || event.ctrlKey) && event.key === 'k') {
      event.preventDefault();
      togglePalette();
      return;
    }

    if (!isOpen) return;

    switch (event.key) {
      case 'Escape':
        closePalette();
        break;
      case 'ArrowDown':
        event.preventDefault();
        isUsingKeyboard = true;
        selectedIndex = (selectedIndex + 1) % filteredItems.length;
        break;
      case 'ArrowUp':
        event.preventDefault();
        isUsingKeyboard = true;
        selectedIndex = selectedIndex === 0 ? filteredItems.length - 1 : selectedIndex - 1;
        break;
      case 'Enter':
        if (filteredItems[selectedIndex]) {
          event.preventDefault();
          navigateToItem(filteredItems[selectedIndex]);
        }
        break;
    }
  }

  function selectItemOnHover(index) {
    isUsingKeyboard = false;
    selectedIndex = index;
  }

  onDestroy(() => {
    if (browser) {
      document.body.style.overflow = '';
    }
  });
</script>

<svelte:window on:keydown={handleGlobalKeydown} />

<div class="command-palette-wrapper" bind:this={paletteElement} use:clickOutside on:clickOutside={closePalette}>
  <button
    class="search-trigger"
    class:active={isOpen}
    on:click={togglePalette}
    aria-label={isOpen ? 'Close command palette' : 'Open command palette'}
    aria-expanded={isOpen}
  >
    <span class="comma-icon">{@html CommaIcon}</span>
    <span class="shortcut">{@html CmdKIcon}</span>
  </button>

  {#if isOpen}
    <div
      class="backdrop-overlay"
      role="button"
      tabindex="-1"
      on:click={closePalette}
      on:keydown={(e) => e.key === 'Escape' && closePalette()}
      aria-label="Close command palette"
    ></div>
    <div class="expanded-content" role="dialog" aria-modal="true">
      <input
        bind:this={searchInputElement}
        type="text"
        class="search-input"
        placeholder="GO..."
        bind:value={searchInput}
        maxlength="30"
        autocomplete="off"
      />

      <div class="nav-items" data-keyboard-active={isUsingKeyboard}>
        {#each filteredItems as item, index}
          <a
            href={item.href}
            class="nav-item"
            class:current={index === currentPageIndex}
            class:selected={index === selectedIndex && index !== currentPageIndex}
            on:click|preventDefault={() => navigateToItem(item)}
            on:mouseenter={() => selectItemOnHover(index)}
          >
            <span class="icon">{@html item.icon}</span>
            <span class="label">{item.label}</span>
          </a>
        {/each}
      </div>
    </div>
  {/if}
</div>

<style>
  .command-palette-wrapper {
    position: relative;
    width: 300px;
    margin: 0 auto;
    z-index: 1000;
  }

  .search-trigger {
    width: 100%;
    height: 48px;
    background-color: #cccccc86;
    backdrop-filter: blur(6px);
    -webkit-backdrop-filter: blur(6px);
    border: 2px solid #3434348f;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 16px;
    cursor: pointer;
    box-shadow: 0 0 2px 1px rgba(27, 27, 27, 0.9) inset;
    font-family: 'JetBrains Mono', monospace;
    position: relative;
    z-index: 1001;
  }

  @media (hover: hover) {
    .search-trigger:hover:not(.active) {
      background-color: #c9c9c9b2;
      box-shadow: 0 0 5px 2px rgba(47, 47, 47, 0.9) inset;
    }
  }

  .search-trigger.active {
    background-color: rgba(42, 42, 42, 0.4);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border: 0;
    border-top: 1px solid #fff;
    border-left: 1px solid #fff;
    border-right: 1px solid #fff;
    box-shadow:
      inset -10px 0 3px -6px rgba(218, 218, 218, 0.25),
      inset  10px 0 3px -6px rgba(218, 218, 218, 0.25),
      inset   0px 10px 3px -6px rgba(218, 218, 218, 0.25);
  }

  .search-trigger.active .comma-icon {
    color: #f4f4f4;
  }

  .search-trigger.active .shortcut {
    color: #b7b7b783;
  }

  .comma-icon {
    width: 9px;
    display: flex;
    align-items: center;
    color: #000;
    flex-shrink: 0;
  }

  .comma-icon :global(svg) {
    width: 100%;
    height: auto;
  }

  .shortcut {
    display: flex;
    align-items: center;
    flex-shrink: 0;
    color: #b7b7b77f;
  }

  .shortcut :global(svg) {
    width: 29px;
    height: 19px;
  }

  .backdrop-overlay {
    position: fixed;
    inset: 0;
    background-color: rgba(0, 0, 0, 0.2);
    z-index: 999;
  }

  .expanded-content {
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    background-color: rgba(42, 42, 42, 0.4);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border: 0;
    border-left: 1px solid #fff;
    border-right: 1px solid #fff;
    border-bottom: 1px solid #fff;
    box-shadow:
      inset -10px 0 3px -6px rgba(218, 218, 218, 0.25),
      inset 10px 0 3px -6px rgba(218, 218, 218, 0.25),
      inset 0 -10px 3px -6px rgba(218, 218, 218, 0.25);
    overflow: hidden;
    z-index: 1000;
    padding: 16px 12px 0;
  }

  .search-input {
    margin-bottom: 16px;
    width: 100%;
    height: 40px;
    background-color: rgba(31, 31, 31, 0.7);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border: 1px solid rgba(64, 64, 64, 0.8);
    padding: 0 16px;
    color: #fff;
    font-size: 16px;
    font-family: 'JetBrains Mono', monospace;
    outline: none;
    text-shadow: 0 1px 2px rgba(0, 0, 0, 0.5);
  }

  .search-input:focus {
    border-color: #51ff00;
  }

  .search-input::placeholder {
    color: #888;
    text-transform: uppercase;
    font-weight: 600;
    letter-spacing: 1px;
  }

  .nav-items {
    padding: 0 0 16px;
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  .nav-item {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px 16px;
    text-decoration: none;
    color: #fff;
    border: 2px solid transparent;
    cursor: pointer;
    text-shadow: 0 1px 4px rgba(0, 0, 0, 0.6);
  }

  .nav-item.current {
    border-color: #fff;
    background-color: rgba(255, 255, 255, 0.15);
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
  }

  .nav-item.selected:not(.current),
  .nav-items[data-keyboard-active="false"] .nav-item:hover {
    background-color: rgba(255, 255, 255, 0.15);
  }

  .icon {
    width: 24px;
    height: 24px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    flex-shrink: 0;
    filter: drop-shadow(0 1px 2px rgba(0, 0, 0, 0.6));
  }

  .icon :global(svg) {
    width: 100%;
    height: 100%;
  }

  .label {
    font-size: 14px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    font-family: 'JetBrains Mono', monospace;
    text-shadow: 0 1px 4px rgba(0, 0, 0, 0.6);
  }

  @media (max-width: 500px) {
    .command-palette-wrapper {
      width: 100%;
      margin: 0;
      padding: 0 1rem;
    }

    .search-trigger.active {
      position: fixed;
      top: 1rem;
      left: 1rem;
      right: 1rem;
      width: auto;
      z-index: 1003;
      margin: 0;
      max-width: calc(100vw - 2rem);
      padding: 0 12px;
      border: 0;
    }

    .search-trigger {
      justify-content: center;
    }

    .shortcut {
      display: none;
    }

    .search-input {
      display: none;
    }

    .expanded-content {
      position: fixed;
      inset: 0;
      width: 100vw;
      height: 100dvh;
      max-height: 100dvh;
      overflow-y: auto;
      z-index: 1002;
      padding-top: 5rem;
      border: 0;
    }

    .nav-items {
      padding-top: 0.5rem;
    }

    .backdrop-overlay {
      background-color: rgba(0, 0, 0, 0.7);
      z-index: 1001;
      backdrop-filter: blur(4px);
      -webkit-backdrop-filter: blur(4px);
    }
  }
</style>
