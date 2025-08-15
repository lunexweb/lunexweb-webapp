<script>
  export let isOpen = false;
  
  function toggleMenu() {
    isOpen = !isOpen;
  }
</script>

<!-- Mobile Menu Toggle Button -->
<button
  class="mobile-menu-toggle"
  on:click={toggleMenu}
  aria-label="{isOpen ? 'Close menu' : 'Open menu'}"
  aria-expanded={isOpen}
  aria-controls="mobile-menu"
  id="mobile-menu-toggle"
  data-menu-toggle
>
  <div class="hamburger-icon">
    <span class="line line-1 {isOpen ? 'open' : ''}"></span>
    <span class="line line-2 {isOpen ? 'open' : ''}"></span>
    <span class="line line-3 {isOpen ? 'open' : ''}"></span>
  </div>
</button>

<style>
  .mobile-menu-toggle {
    position: relative;
    width: 44px;
    height: 44px;
    background: #000000;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s ease;
    z-index: 1000;
  }
  
  /* Hide on desktop */
  @media (min-width: 1024px) {
    .mobile-menu-toggle {
      display: none;
    }
  }
  
  .mobile-menu-toggle:hover {
    background: #1f2937;
    transform: scale(1.05);
  }
  
  .mobile-menu-toggle:active {
    transform: scale(0.95);
  }
  
  .mobile-menu-toggle:focus {
    outline: none;
    box-shadow: 0 0 0 3px rgba(0, 0, 0, 0.1);
  }
  
  .hamburger-icon {
    position: relative;
    width: 20px;
    height: 16px;
  }
  
  .line {
    position: absolute;
    left: 0;
    width: 20px;
    height: 2px;
    background: #ffffff;
    border-radius: 1px;
    transition: all 0.3s ease;
    transform-origin: center;
  }
  
  .line-1 {
    top: 0;
  }
  
  .line-2 {
    top: 50%;
    transform: translateY(-50%);
  }
  
  .line-3 {
    bottom: 0;
  }
  
  /* Animation for open state */
  .line-1.open {
    transform: rotate(45deg) translate(6px, 6px);
  }
  
  .line-2.open {
    opacity: 0;
    transform: translateX(-20px);
  }
  
  .line-3.open {
    transform: rotate(-45deg) translate(6px, -6px);
  }
  
  /* Ensure touch target is large enough */
  @media (max-width: 480px) {
    .mobile-menu-toggle {
      width: 48px;
      height: 48px;
    }
    
    .hamburger-icon {
      width: 22px;
      height: 18px;
    }
    
    .line {
      width: 22px;
      height: 2px;
    }
  }
</style> 