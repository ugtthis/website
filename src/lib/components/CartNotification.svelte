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
    min-width: auto;
    height: 32px;
    background-color: rgba(4, 255, 0, 0.95);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border: 2px solid #333333;
    border-radius: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    padding: 0 12px;
    cursor: pointer;
    transition: all 0.2s;
    box-sizing: border-box;
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
    background-color: rgba(42, 42, 42, 1);
    border-color: #51ff00;
  }

  .cart-notification:hover .cart-label,
  .cart-notification:hover .cart-badge {
    color: #51ff00;
  }

  .cart-notification:active {
    transform: scale(0.95);
  }

  .cart-label {
    color: #000000;
    font-size: 12px;
    font-weight: 600;
    font-family: Inter, sans-serif;
    line-height: 1;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .cart-badge {
    color: #000000;
    font-size: 12px;
    font-weight: 600;
    font-family: Inter, sans-serif;
    line-height: 1;
    text-align: center;
  }
</style>
