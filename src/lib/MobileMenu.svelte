<script>
  import { createEventDispatcher } from 'svelte';
  import { page } from '$app/stores';
  import { browser } from '$app/environment';
  import { onDestroy } from 'svelte';
  
  const dispatch = createEventDispatcher();
  
  export let isOpen = false;
  
  // Close menu when route changes
  let previousPath = '';
  let isNavigating = false;
  
  // Watch for route changes and close menu immediately
  $: if ($page.url.pathname !== previousPath) {
    if (previousPath !== '') {
      // Immediately close menu on route change
      isNavigating = true;
      isOpen = false;
      cleanupBodyScroll();
      
      // Reset navigation state after cleanup
      setTimeout(() => {
        isNavigating = false;
      }, 150);
    }
    previousPath = $page.url.pathname;
  }
  
  function closeMenu() {
    if (isNavigating) return; // Prevent closing during navigation
    isOpen = false;
    cleanupBodyScroll();
    dispatch('close');
  }
  
  function cleanupBodyScroll() {
    if (browser) {
      document.body.classList.remove('menu-open');
    }
  }
  
  // Prevent body scroll when menu is open
  $: if (isOpen && browser) {
    document.body.classList.add('menu-open');
  } else if (browser) {
    cleanupBodyScroll();
  }
  
  // Navigation guard - prevent menu from opening during navigation
  $: if (isNavigating && isOpen) {
    isOpen = false;
    cleanupBodyScroll();
  }
  
  // Safety timeout - ensure menu can't get stuck open
  let safetyTimeout;
  $: if (isOpen && browser) {
    if (safetyTimeout) clearTimeout(safetyTimeout);
    safetyTimeout = setTimeout(() => {
      if (isOpen) {
        console.warn('Mobile menu safety timeout triggered - forcing close');
        closeMenu();
      }
    }, 30000); // 30 seconds
  } else if (browser && safetyTimeout) {
    clearTimeout(safetyTimeout);
  }
  
  // Global menu state reset function
  function forceResetMenu() {
    isOpen = false;
    isNavigating = false;
    cleanupBodyScroll();
    if (safetyTimeout) clearTimeout(safetyTimeout);
    console.log('Mobile menu force reset completed');
  }
  
  // Expose reset function globally for emergency use
  if (browser) {
    window.resetMobileMenu = forceResetMenu;
  }
  
  // Safety mechanism - ensure menu can always be closed
  let cleanupListeners;
  if (browser) {
    const beforeUnloadHandler = () => cleanupBodyScroll();
    const popStateHandler = () => {
      if (isOpen) {
        closeMenu();
      }
    };
    const clickOutsideHandler = (e) => {
      if (isOpen && !isNavigating && !e.target.closest('.mobile-menu-content') && !e.target.closest('[data-menu-toggle]')) {
        closeMenu();
      }
    };
    
    window.addEventListener('beforeunload', beforeUnloadHandler);
    window.addEventListener('popstate', popStateHandler);
    document.addEventListener('click', clickOutsideHandler);
    
    cleanupListeners = () => {
      window.removeEventListener('beforeunload', beforeUnloadHandler);
      window.removeEventListener('popstate', popStateHandler);
      document.removeEventListener('click', clickOutsideHandler);
      if (safetyTimeout) {
        clearTimeout(safetyTimeout);
      }
    };
  }
  
  // Cleanup on component destroy
  onDestroy(() => {
    // Force close menu and cleanup
    isOpen = false;
    isNavigating = false;
    cleanupBodyScroll();
    if (cleanupListeners) {
      cleanupListeners();
    }
    // Clear all timeouts
    if (safetyTimeout) clearTimeout(safetyTimeout);
  });
</script>

<!-- Mobile Menu Overlay -->
{#if isOpen}
  <div 
    class="mobile-menu-overlay"
    on:click={closeMenu}
    on:keydown={(e) => e.key === 'Escape' && closeMenu()}
    role="dialog"
    aria-modal="true"
    aria-label="Mobile navigation menu"
    tabindex="-1"
  >
    <!-- Mobile Menu Content -->
    <div 
      class="mobile-menu-content"
      role="region"
      aria-label="Mobile menu content"
    >
      <!-- Close Button -->
      <button
        class="close-button"
        on:click={closeMenu}
        aria-label="Close menu"
      >
        <svg class="close-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
        </svg>
      </button>
      
      <!-- Logo in Menu -->
      <div class="logo-section">
        <a href="/" class="logo-link">
          <div class="logo-circle">
            <span class="logo-text">L</span>
          </div>
          <span class="logo-brand">LunexWeb</span>
        </a>
      </div>
      
      <!-- Navigation Links -->
      <nav class="mobile-nav">
        <a 
          href="/" 
          class="mobile-nav-link {$page.url.pathname === '/' ? 'mobile-nav-link-active' : ''}"
        >
          Home
        </a>
        <a 
          href="/about" 
          class="mobile-nav-link {$page.url.pathname === '/about' ? 'mobile-nav-link-active' : ''}"
        >
          About
        </a>
        <a 
          href="/websites" 
          class="mobile-nav-link {$page.url.pathname === '/websites' ? 'mobile-nav-link-active' : ''}"
        >
          Websites & Marketing
        </a>
        <a 
          href="/packages" 
          class="mobile-nav-link {$page.url.pathname === '/packages' ? 'mobile-nav-link-active' : ''}"
        >
          Packages
        </a>
        <a 
          href="/contact" 
          class="mobile-nav-link {$page.url.pathname === '/contact' ? 'mobile-nav-link-active' : ''}"
        >
          Contact
        </a>
      </nav>
      
      <!-- Contact Info -->
      <div class="contact-section">
        <div class="contact-content">
          <p class="location">📍 Johannesburg, South Africa</p>
          <a 
            href="https://www.instagram.com/lunexweb?igsh=ZzE2OGhkNDk5d2p6" 
            target="_blank" 
            rel="noopener noreferrer"
            class="instagram-link"
          >
            <svg class="instagram-icon" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
            </svg>
            <span>Follow us on Instagram</span>
          </a>
        </div>
      </div>
    </div>
  </div>
{/if}

<style>
  /* Mobile Menu Overlay - Full screen with bottom positioning */
  .mobile-menu-overlay {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.8);
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
    z-index: 9999;
    animation: fadeIn 0.3s ease-out;
    touch-action: none;
    overflow: hidden;
  }
  
  /* Mobile Menu Content - Bottom positioned like mobile app */
  .mobile-menu-content {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    width: 100%;
    background: white;
    border-radius: 20px 20px 0 0;
    padding: 2rem 1.5rem 1.5rem;
    overflow-y: auto;
    animation: slideUpFromBottom 0.3s ease-out;
    box-shadow: 0 -4px 20px rgba(0, 0, 0, 0.2);
    max-height: 85vh;
  }
  
  /* Close Button */
  .close-button {
    position: absolute;
    top: 1rem;
    right: 1.5rem;
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    background: #f3f4f6;
    border: none;
    cursor: pointer;
    transition: all 0.2s ease;
    z-index: 10;
  }
  
  .close-button:hover {
    background: #e5e7eb;
    transform: scale(1.05);
  }
  
  .close-icon {
    width: 20px;
    height: 20px;
    color: #6b7280;
  }
  
  /* Logo Section */
  .logo-section {
    margin-bottom: 2rem;
    padding-top: 1rem;
    text-align: center;
  }
  
  .logo-link {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.75rem;
    text-decoration: none;
    color: inherit;
  }
  
  .logo-circle {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: #000000;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .logo-text {
    color: white;
    font-weight: 900;
    font-size: 1.25rem;
  }
  
  .logo-brand {
    font-size: 1.25rem;
    font-weight: 900;
    color: #000000;
  }
  
  /* Mobile Navigation */
  .mobile-nav {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin-bottom: 2rem;
  }
  
  .mobile-nav-link {
    display: block;
    padding: 1rem 1.25rem;
    font-size: 1.125rem;
    font-weight: 500;
    color: #000000;
    text-decoration: none;
    border-radius: 12px;
    transition: all 0.3s ease;
    position: relative;
    min-height: 48px;
    display: flex;
    align-items: center;
  }
  
  .mobile-nav-link::before {
    content: '';
    position: absolute;
    left: 0;
    top: 0;
    width: 0;
    height: 100%;
    background: rgba(0, 0, 0, 0.05);
    border-radius: 12px;
    transition: width 0.3s ease;
  }
  
  .mobile-nav-link:hover::before {
    width: 100%;
  }
  
  .mobile-nav-link:hover {
    transform: translateX(8px);
  }
  
  .mobile-nav-link-active {
    background: rgba(0, 0, 0, 0.05);
  }
  
  .mobile-nav-link-active::before {
    width: 100%;
  }
  
  /* Contact Section */
  .contact-section {
    padding-top: 1.5rem;
    border-top: 1px solid #e5e7eb;
  }
  
  .contact-content {
    text-align: center;
  }
  
  .location {
    font-size: 0.875rem;
    color: #6b7280;
    margin-bottom: 0.75rem;
  }
  
  .instagram-link {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 0.875rem;
    color: #6b7280;
    text-decoration: none;
    transition: color 0.2s ease;
  }
  
  .instagram-link:hover {
    color: #000000;
  }
  
  .instagram-icon {
    width: 20px;
    height: 20px;
  }
  
  /* Animations */
  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
  
  @keyframes slideUpFromBottom {
    from {
      transform: translateY(100%);
    }
    to {
      transform: translateY(0);
    }
  }
  
  /* Responsive adjustments */
  @media (max-width: 480px) {
    .mobile-menu-content {
      padding: 1.5rem 1rem 1rem;
      border-radius: 16px 16px 0 0;
    }
    
    .mobile-nav-link {
      padding: 0.875rem 1rem;
      font-size: 1rem;
    }
    
    .logo-section {
      margin-bottom: 1.5rem;
    }
  }
  
  /* Ensure touch targets are large enough */
  .mobile-nav-link,
  .close-button {
    min-height: 48px;
    min-width: 48px;
  }
  
  /* Body scroll prevention */
  :global(body.menu-open) {
    overflow: hidden;
    position: fixed;
    width: 100%;
  }
</style> 