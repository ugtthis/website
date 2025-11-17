<script>
  import { createEventDispatcher } from 'svelte';
  import { cartTotalQuantity } from '../../store.js';

  const dispatch = createEventDispatcher();
</script>

<button
  class="cart-notification"
  on:click={() => dispatch('click')}
  aria-label={`Cart with {$cartTotalQuantity} item{$cartTotalQuantity === 1 ? '' : 's'}`}
>
  <span class="cart-label">Cart</span>
  <span class="cart-badge">{$cartTotalQuantity}</span>
</button>

<style>
  .cart-notification {
    position: relative;
    height: 32px;
    background-color: rgba(4, 255, 0, 0.95);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border: 3px solid #123315;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    padding: 0 12px;
    cursor: pointer;
    transition: all 0.2s;
    animation: slideIn 0.3s ease-out;
  }

  @media (max-width: 500px) {
    .cart-notification {
      margin-right: 1rem;
    }
  }

  @keyframes slideIn {
    from {
      opacity: 0;
      transform: translateX(-10px);
    }
    to {
      opacity: 1;
      transform: translateX(0);
    }
  }

  .cart-notification:hover {
    background-color: rgb(0, 0, 0);
    border-color: #51ff00;
  }

  .cart-notification:hover .cart-label,
  .cart-notification:hover .cart-badge {
    color: #6cea31;
  }

  .cart-notification:active {
    transform: scale(0.95);
  }

  .cart-label,
  .cart-badge {
    color: rgb(41, 41, 41);
    font-size: 12px;
    font-weight: 600;
    font-family: Inter, sans-serif;
    text-transform: uppercase;
  }

  @media (max-width: 500px) {
    .cart-label,
    .cart-badge {
      font-size: 14px;
    }
  }
</style>
