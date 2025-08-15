<script>
  import { onMount } from 'svelte';
  import { page } from '$app/stores';
  import '../app.css';
  import MobileMenu from '../lib/MobileMenu.svelte';
  import MobileMenuToggle from '../lib/MobileMenuToggle.svelte';
  
  let lenis;
  let isScrolled = false;
  let mobileMenuOpen = false;
  
  onMount(() => {
    // Initialize Lenis for smooth scrolling with error handling
    const initLenis = async () => {
      try {
        const Lenis = (await import('lenis')).default;
        lenis = new Lenis({
          duration: 1.2,
          easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
          touchMultiplier: 2,
        });
        
        function raf(time) {
          lenis.raf(time);
          requestAnimationFrame(raf);
        }
        
        requestAnimationFrame(raf);
      } catch (error) {
        console.warn('Lenis initialization failed:', error);
        // Continue without smooth scrolling
      }
    };
    
    initLenis();
    
    // Handle scroll effects for header
    const handleScroll = () => {
      isScrolled = window.scrollY > 10;
    };
    
    window.addEventListener('scroll', handleScroll);
    
    // Cleanup on unmount
    return () => {
      try {
        if (lenis) {
          lenis.destroy();
        }
      } catch (error) {
        console.warn('Lenis cleanup failed:', error);
      }
      window.removeEventListener('scroll', handleScroll);
    };
  });
</script>

<svelte:head>
  <title>LunexWeb - Modern Websites & Marketing That Deliver Results | Johannesburg, South Africa</title>
  <meta name="description" content="LunexWeb delivers professional web development and digital marketing services in Johannesburg, South Africa. Expert web development, SEO optimization, Google Ads, and social media management." />
  <meta name="keywords" content="web development Johannesburg, digital marketing South Africa, modern websites, business websites, SEO services, Google Ads, social media management" />
  <meta name="robots" content="index, follow" />
  <meta name="author" content="LunexWeb" />
  <meta property="og:type" content="website" />
  <meta property="og:title" content="LunexWeb - Modern Websites & Marketing That Deliver Results" />
  <meta property="og:description" content="Professional web development and digital marketing services in Johannesburg, South Africa. Creating sleek, modern designs tailored to your business needs." />
  <meta property="og:site_name" content="LunexWeb" />
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content="LunexWeb - Modern Websites & Marketing That Deliver Results" />
  <meta name="twitter:description" content="Professional web development and digital marketing services in Johannesburg, South Africa. Creating sleek, modern designs tailored to your business needs." />
  
  <!-- Mobile Viewport Meta Tag - Essential for mobile responsiveness -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  
  <!-- Structured Data Schema -->
  <script type="application/ld+json">
    {
      "@context": "https://schema.org",
      "@type": "LocalBusiness",
      "name": "LunexWeb",
      "description": "Professional web development and digital marketing services in Johannesburg, South Africa. Creating modern, responsive websites that deliver real business results.",
      "url": "https://lunexweb.com",
      "telephone": "+27-XX-XXX-XXXX",
      "email": "inquiry@lunexweb.com",
      "address": {
        "@type": "PostalAddress",
        "addressLocality": "Johannesburg",
        "addressCountry": "ZA",
        "addressRegion": "Gauteng"
      },
      "geo": {
        "@type": "GeoCoordinates",
        "latitude": -26.2041,
        "longitude": 28.0473
      },
      "openingHours": "Mo-Fr 09:00-17:00",
      "priceRange": "$$",
      "serviceArea": {
        "@type": "GeoCircle",
        "geoMidpoint": {
          "@type": "GeoCoordinates",
          "latitude": -26.2041,
          "longitude": 28.0473
        },
        "geoRadius": "50000"
      },
      "hasOfferCatalog": {
        "@type": "OfferCatalog",
        "name": "Web Development & Digital Marketing Services",
        "itemListElement": [
          {
            "@type": "Offer",
            "itemOffered": {
              "@type": "Service",
              "name": "Web Development",
              "description": "Modern, responsive websites built with React, Svelte, HTML5, CSS3, JavaScript, and Tailwind CSS"
            }
          },
          {
            "@type": "Offer",
            "itemOffered": {
              "@type": "Service",
              "name": "Digital Marketing",
              "description": "SEO optimization, Google Ads management, social media advertising, and social media management"
            }
          }
        ]
      }
    }
  </script>
</svelte:head>

<!-- Modern Header -->
<header class="modern-header {isScrolled ? 'header-scrolled' : ''}">
  <div class="header-container">
    <div class="header-content">
      <!-- Logo -->
      <a href="/" class="header-logo">
        <div class="logo-circle">
          <span class="logo-text">L</span>
        </div>
        <span class="logo-brand">LunexWeb</span>
      </a>
      
      <!-- Desktop Navigation -->
      <nav class="header-nav-desktop">
        <a href="/" class="nav-link {$page.url.pathname === '/' ? 'nav-link-active' : ''}">
          Home
        </a>
        <a href="/about" class="nav-link {$page.url.pathname === '/about' ? 'nav-link-active' : ''}">
          About
        </a>
        <a href="/websites" class="nav-link {$page.url.pathname === '/websites' ? 'nav-link-active' : ''}">
          Websites & Marketing
        </a>
        <a href="/packages" class="nav-link {$page.url.pathname === '/packages' ? 'nav-link-active' : ''}">
          Packages
        </a>
        <a href="/contact" class="nav-link {$page.url.pathname === '/contact' ? 'nav-link-active' : ''}">
          Contact
        </a>
      </nav>
      
      <!-- Mobile Menu Toggle -->
      <MobileMenuToggle bind:isOpen={mobileMenuOpen} class="lg:hidden" />
    </div>
  </div>
  </header>

<!-- Mobile Menu - Hidden on desktop -->
<div class="lg:hidden">
  <MobileMenu 
    bind:isOpen={mobileMenuOpen}
    on:close={() => mobileMenuOpen = false}
  />
</div>

<!-- Main Content -->
<main>
  <slot />
</main>

<!-- Footer -->
<footer class="bg-black text-white py-12">
  <div class="container-custom px-4 text-center">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mb-8">
      <div>
        <h3 class="text-xl font-bold mb-4">LunexWeb</h3>
        <p class="text-gray-300 mb-4">Professional web development and digital marketing services in Johannesburg, South Africa. We create sleek, modern designs tailored to your business needs, helping you stand out and attract customers.</p>
        <p class="text-gray-400 text-sm">📍 Johannesburg, South Africa</p>
      </div>
      <div>
        <h4 class="text-lg font-semibold mb-4">Quick Links</h4>
        <div class="flex flex-col space-y-2">
          <a href="/" class="text-gray-300 hover:text-white transition-colors">Home</a>
          <a href="/about" class="text-gray-300 hover:text-white transition-colors">About</a>
          <a href="/websites" class="text-gray-300 hover:text-white transition-colors">Websites & Marketing</a>
                  <a href="/packages" class="text-gray-300 hover:text-white transition-colors">Our Packages</a>
        <a href="/contact" class="text-gray-300 hover:text-white transition-colors">Contact</a>
        </div>
      </div>
      <div>
        <h4 class="text-lg font-semibold mb-4">Services</h4>
        <div class="flex flex-col space-y-2">
          <a href="/websites" class="text-gray-300 hover:text-white transition-colors">Web Development</a>
          <a href="/websites" class="text-gray-300 hover:text-white transition-colors">Digital Marketing</a>
          <a href="/websites" class="text-gray-300 hover:text-white transition-colors">SEO Services</a>
          <a href="/websites" class="text-gray-300 hover:text-white transition-colors">Social Media Management</a>
        </div>
        <div class="mt-4">
          <h5 class="text-md font-semibold mb-2">Connect</h5>
          <div class="flex space-x-4 justify-center">
            <a href="https://www.instagram.com/lunexweb?igsh=ZzE2OGhkNDk5d2p6" target="_blank" rel="noopener noreferrer" class="text-gray-300 hover:text-white transition-colors">
              <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
                <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
              </svg>
            </a>
          </div>
        </div>
      </div>
    </div>
    <div class="border-t border-gray-600 pt-8">
      <p class="text-gray-300 text-sm">
        © 2024 LunexWeb. Professional web development and digital marketing services in Johannesburg, South Africa.
      </p>
    </div>
  </div>
</footer> 