<script>
  import { onMount, onDestroy } from 'svelte';
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
    { label: 'SUPPORT', href: '/support', icon: SupportQuestionIcon }
  ];

  $: currentPath = $page.url.pathname;
  $: currentPageItem = navItems.reduce((match, item) => {
    if (item.external) return match;
    const pathMatches = item.href === '/'
      ? currentPath === '/'
      : currentPath === item.href || currentPath.startsWith(item.href + '/');
    return pathMatches && item.href.length > (match?.href.length || 0) ? item : match;
  }, null);
  $: highlightedIndex = currentPageItem ? filteredItems.indexOf(currentPageItem) : -1;

  let isOpen = false;
  let searchInput = '';
  let selectedIndex = 0;
  let searchInputElement;
  let paletteElement;
  let isKeyboardNavigation = false;

  $: filteredItems = navItems.filter(item =>
    item.label.toLowerCase().includes(searchInput.toLowerCase())
  );

  $: if (filteredItems.length > 0 && selectedIndex >= filteredItems.length) {
    selectedIndex = 0;
  }

  // Disable body scroll when palette is open on mobile
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
      selectedIndex = Math.max(0, highlightedIndex);
      searchInput = '';
      isKeyboardNavigation = false;
      if (browser) {
        // Prevent Safari URL bar from hiding when opening menu on mobile
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
    isKeyboardNavigation = false;
  }

  function handleKeydown(event) {
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
        isKeyboardNavigation = true;
        selectedIndex = (selectedIndex + 1) % filteredItems.length;
        break;
      case 'ArrowUp':
        event.preventDefault();
        isKeyboardNavigation = true;
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

  onMount(() => {
    if (browser) {
      document.addEventListener('keydown', handleKeydown);
    }
  });

  onDestroy(() => {
    if (browser) {
      document.removeEventListener('keydown', handleKeydown);
      document.body.style.overflow = '';
    }
  });
</script>

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
      <div class="search-container">
        <input
          bind:this={searchInputElement}
          type="text"
          class="search-input"
          placeholder="GO ..."
          bind:value={searchInput}
          maxlength="30"
          autocomplete="off"
        />
      </div>

      <div class="nav-items" class:keyboard-navigation={isKeyboardNavigation}>
        {#each filteredItems as item, index}
          <a
            href={item.href}
            class="nav-item"
            class:highlighted={index === highlightedIndex}
            class:selected={index === selectedIndex && index !== highlightedIndex}
            on:click|preventDefault={() => navigateToItem(item)}
            on:mouseenter={() => {
              if (isKeyboardNavigation) {
                isKeyboardNavigation = false;
              } else {
                selectedIndex = index;
              }
            }}
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

  /* Button when closed */
  .search-trigger {
    width: 100%;
    height: 48px;
    background-color: #cccccc86;
    backdrop-filter: blur(6px);
    -webkit-backdrop-filter: blur(6px);
    border: 2px solid #3434348f;
    border-radius: 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 16px;
    cursor: pointer;
    box-shadow: 0 0 2px 1px rgba(27, 27, 27, 0.9) inset;
    transition: all 0.2s ease-in-out;
    font-family: 'JetBrains Mono', monospace;
    position: relative;
    z-index: 1001;
  }

  /* Hover effect - desktop only (not mobile) */
  @media (hover: hover) {
    .search-trigger:hover:not(.active) {
      background-color: #c9c9c9b2;
      box-shadow: 0 0 5px 2px rgba(47, 47, 47, 0.9) inset;
    }
  }

  /* Button when expanded/open */
  .search-trigger.active {
    background-color: rgba(42, 42, 42, 0.4);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border: none;
    box-shadow: none;
  }

  .search-trigger.active .comma-icon {
    flex-shrink: 0;
    color: #f4f4f4;
    transition: color 0.2s ease-in-out;
  }

  .search-trigger.active .shortcut {
    color: #b7b7b783;
    transition: color 0.2s ease-in-out;
  }

  .comma-icon {
    width: 9px;
    height: auto;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    color: #000;
  }

  .comma-icon :global(svg) {
    width: 9px;
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

  /* Backdrop Overlay */
  .backdrop-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.2);
    z-index: 999;
    animation: fadeIn 0.2s ease-out;
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }

  /* Expanded Content */
  .expanded-content {
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    background-color: rgba(42, 42, 42, 0.4);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border: none;
    border-radius: 0;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.5);
    overflow: hidden;
    animation: expandDown 0.3s ease-out;
    z-index: 1000;
  }

  @keyframes expandDown {
    from {
      opacity: 0;
      transform: translateY(-10px);
      max-height: 0;
    }
    to {
      opacity: 1;
      transform: translateY(0);
      max-height: 600px;
    }
  }

  /* Search Container */
  .search-container {
    padding: 16px 20px;
  }

  .search-input {
    width: 100%;
    height: 48px;
    background-color: rgba(31, 31, 31, 0.7);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border: 1px solid rgba(64, 64, 64, 0.8);
    border-radius: 0;
    padding: 0 16px;
    color: #fff;
    font-size: 16px;
    font-family: 'JetBrains Mono', monospace;
    outline: none;
    transition: border-color 0.2s;
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

  /* Navigation Items */
  .nav-items {
    padding: 0 12px 16px;
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  .nav-item {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px 16px;
    border-radius: 0;
    text-decoration: none;
    color: #fff;
    transition: all 0.15s;
    border: 2px solid transparent;
    cursor: pointer;
    text-shadow: 0 1px 4px rgba(0, 0, 0, 0.6);
  }

  .nav-item.highlighted {
    border-color: #fff;
    background-color: rgba(255, 255, 255, 0.15);
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
  }

  .nav-item.selected:not(.highlighted) {
    background-color: rgba(255, 255, 255, 0.15);
  }

  /* Hover disabled when using keyboard navigation */
  .nav-items:not(.keyboard-navigation) .nav-item:hover {
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

  /* Responsive - Mobile */
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
    }

    .search-trigger {
      justify-content: center;
    }

    .shortcut {
      display: none;
    }

    .search-container {
      display: none;
    }

    .expanded-content {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      width: 100vw;
      height: 100dvh;
      max-height: 100dvh;
      overflow-y: auto;
      z-index: 1002;
      animation: fadeIn 0.2s ease-out;
      padding-top: 5rem;
    }

    .nav-items {
      padding-top: 0.5rem;
    }

    .backdrop-overlay {
      background-color: rgba(0, 0, 0, 0.7);
      z-index: 1001;
    }
  }
</style>
