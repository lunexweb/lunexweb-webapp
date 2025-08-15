<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  import OptimizedVideo from '$lib/OptimizedVideo.svelte';
  
  gsap.registerPlugin(ScrollTrigger);
  
  let introSection;
  let horizontalScroll;
  let sections;
  let currentTime = '';
  let mobileCarousel;
  let currentSlide = 0;
  let startX = 0;
  let currentX = 0;
  let isDragging = false;
  
  // Carousel functions
  function nextSlide() {
    if (currentSlide < 2) {
      currentSlide++;
    }
  }
  
  function previousSlide() {
    if (currentSlide > 0) {
      currentSlide--;
    }
  }
  
  function goToSlide(index) {
    currentSlide = index;
  }
  
  // Touch handlers for mobile carousel
  function handleTouchStart(e) {
    startX = e.touches[0].clientX;
    isDragging = true;
  }
  
  function handleTouchMove(e) {
    if (!isDragging) return;
    currentX = e.touches[0].clientX;
  }
  
  function handleTouchEnd() {
    if (!isDragging) return;
    
    const diff = startX - currentX;
    const threshold = 50; // Minimum swipe distance
    
    if (Math.abs(diff) > threshold) {
      if (diff > 0 && currentSlide < 2) {
        // Swipe left - next slide
        nextSlide();
      } else if (diff < 0 && currentSlide > 0) {
        // Swipe right - previous slide
        previousSlide();
      }
    }
    
    isDragging = false;
  }
  
  onMount(() => {
    // Update time every second
    const updateTime = () => {
      const now = new Date();
      currentTime = now.toLocaleTimeString('en-US', { 
        hour12: false, 
        hour: '2-digit', 
        minute: '2-digit',
        second: '2-digit',
        timeZone: 'Africa/Johannesburg'
      });
    };
    
    updateTime();
    const timeInterval = setInterval(updateTime, 1000);
    
    // Auto-advance carousel on mobile
    let carouselInterval;
    if (window.innerWidth < 1024) {
      carouselInterval = setInterval(() => {
        if (currentSlide < 2) {
          currentSlide++;
        } else {
          currentSlide = 0;
        }
      }, 8000); // Change slide every 8 seconds
    }
    
    // Handle window resize for responsive behavior
    const handleResize = () => {
      // Re-initialize horizontal scroll if switching to desktop
      if (window.innerWidth >= 1024 && horizontalScroll) {
        const totalWidth = horizontalScroll.scrollWidth - horizontalScroll.clientWidth;
        
        gsap.to(horizontalScroll, {
          x: -totalWidth,
          ease: "none",
          scrollTrigger: {
            trigger: horizontalScroll,
            start: "top top",
            end: `+=${totalWidth}`,
            scrub: 0.5,
            pin: true
          }
        });
      }
      
      // Clear carousel interval if switching to desktop
      if (window.innerWidth >= 1024) {
        if (carouselInterval) {
          clearInterval(carouselInterval);
          carouselInterval = null;
        }
      } else if (!carouselInterval) {
        // Start carousel interval if switching to mobile
        carouselInterval = setInterval(() => {
          if (currentSlide < 2) {
            currentSlide++;
          } else {
            currentSlide = 0;
          }
        }, 8000);
      }
    };
    
    window.addEventListener('resize', handleResize);
    
    // Intro animation sequence - very fast (1 second total)
    const introTexts = ['Welcome', 'Design', 'Code', 'Launch'];
    let currentIndex = 0;
    
    const animateIntro = () => {
      if (currentIndex < introTexts.length) {
        // Very quick fade out
        gsap.to(introSection.querySelector('.intro-text'), {
          duration: 0.1,
          opacity: 0,
          ease: "power2.out",
          onComplete: () => {
            introSection.querySelector('.intro-text').textContent = introTexts[currentIndex];
            // Very quick fade in
            gsap.to(introSection.querySelector('.intro-text'), {
              duration: 0.1,
              opacity: 1,
              ease: "power2.out"
            });
            currentIndex++;
            // Very fast transition between words (1 second total = 250ms per word)
            setTimeout(animateIntro, 150);
          }
        });
      } else {
        // Quick fade out intro and show main content
        gsap.to(introSection, {
          duration: 0.2,
          opacity: 0,
          ease: "power2.out",
          onComplete: () => {
            introSection.style.display = 'none';
            gsap.to('.main-content', {
              duration: 0.2,
              opacity: 1,
              ease: "power2.out"
            });
          }
        });
      }
    };
    
    // Start intro animation immediately
    animateIntro();
    
    // Horizontal scroll setup - lightweight (desktop only)
    if (horizontalScroll && window.innerWidth >= 1024) {
      const totalWidth = horizontalScroll.scrollWidth - horizontalScroll.clientWidth;
      
      gsap.to(horizontalScroll, {
        x: -totalWidth,
        ease: "none",
        scrollTrigger: {
          trigger: horizontalScroll,
          start: "top top",
          end: `+=${totalWidth}`,
          scrub: 0.5,
          pin: true
        }
      });
    }
    
    // Simple section animations - lightweight and reliable
    
    // Section animations - lightweight
    if (sections) {
      sections.forEach((section, index) => {
        gsap.fromTo(section, 
          { opacity: 0, y: 50 },
          { 
            opacity: 1, 
            y: 0, 
            duration: 0.6, 
            ease: "power2.out",
            scrollTrigger: {
              trigger: section,
              start: "top 80%",
              toggleActions: "play none none none"
            }
          }
        );
      });
    }
    
    // Cleanup function
    const cleanup = () => {
      clearInterval(timeInterval);
      if (carouselInterval) {
        clearInterval(carouselInterval);
      }
      window.removeEventListener('resize', handleResize);
    };
    
    // Cleanup on unmount
    return cleanup;
  });
</script>

<svelte:head>
  <title>LunexWeb — Modern Websites & Marketing That Deliver Results | Johannesburg</title>
  <meta name="description" content="LunexWeb creates sleek, modern designs tailored to your business needs in Johannesburg, South Africa. Specializing in web development and digital marketing that bring real returns on investment." />
  <meta name="keywords" content="web development Johannesburg, digital marketing South Africa, modern websites, business websites, SEO services, Google Ads, social media marketing" />
</svelte:head>

<!-- Intro Section -->
<section bind:this={introSection} class="fixed inset-0 z-50 flex items-center justify-center bg-primary">
  <div class="text-center px-4">
    <h1 class="intro-text text-2xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl font-light text-text tracking-wider">
      Welcome
    </h1>
  </div>
</section>

<!-- Main Content -->
<div class="main-content opacity-0">
  <!-- Hero Section -->
  <section class="min-h-screen flex items-center justify-center bg-white relative overflow-hidden">
    <!-- Background Video -->
    <div class="absolute inset-0 z-0">
      <OptimizedVideo
        src="https://res.cloudinary.com/dnnwvmh3n/video/upload/v1755168848/main_background_1_tjweeu.mp4"
        autoplay={true}
        muted={true}
        loop={true}
        playsinline={true}
        preload="auto"
        class_name="w-full h-full"
        objectFit="cover"
        objectPosition="center"
        alt="Modern web development and digital marketing background video"
      />
      <!-- Video overlay for better text readability -->
      <div class="absolute inset-0 bg-black/20"></div>
    </div>
    
    <div class="container-custom text-center px-4 sm:px-6 md:px-8 relative z-10">
      <h1 class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl xl:text-7xl 2xl:text-8xl font-bold text-white mb-6 sm:mb-8 leading-tight">
        Modern Web Development & Digital Marketing
      </h1>
      <p class="text-xl sm:text-2xl md:text-3xl lg:text-4xl text-white/90 mb-8 sm:mb-10 lg:mb-12 max-w-2xl sm:max-w-3xl lg:max-w-4xl mx-auto leading-relaxed">
        LunexWeb — Modern Websites & Marketing That Deliver Results
      </p>
      <p class="text-lg sm:text-xl md:text-2xl lg:text-3xl text-white/80 mb-8 sm:mb-10 lg:mb-12 max-w-2xl sm:max-w-3xl lg:max-w-4xl mx-auto leading-relaxed">
        We create sleek, modern designs tailored to your business needs, helping you stand out and attract customers.
      </p>
      <p class="text-base sm:text-lg md:text-xl lg:text-2xl text-white/70 mb-8 sm:mb-10 lg:mb-12 max-w-2xl sm:max-w-3xl lg:max-w-4xl mx-auto leading-relaxed">
        At LunexWeb, we specialise in web development and digital marketing that bring real returns on investment. From business profiles to complete digital strategies, we deliver results-driven solutions that help you grow.
      </p>
    </div>
    
    <!-- Location and Time Card - Centered at bottom -->
    <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2 z-20">
      <div class="bg-white/10 backdrop-blur-md border border-white/20 rounded-2xl px-6 py-4 shadow-2xl">
        <div class="flex flex-col sm:flex-row items-center space-y-2 sm:space-y-0 sm:space-x-4 text-white">
          <div class="flex items-center space-x-2">
            <svg class="w-5 h-5 text-white/80" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z"/>
            </svg>
            <span class="text-sm sm:text-base font-medium">Johannesburg | South Africa</span>
          </div>
          <div class="flex items-center space-x-2">
            <svg class="w-5 h-5 text-white/80" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>
            </svg>
            <span class="text-sm sm:text-base font-mono font-medium">{currentTime}</span>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Background decorative elements -->
    <div class="absolute inset-0 opacity-5 z-5 hidden md:block">
      <div class="absolute top-20 left-20 w-24 h-24 lg:w-32 lg:h-32 bg-gray-200 rounded-full"></div>
      <div class="absolute bottom-20 right-20 w-20 h-20 lg:w-24 lg:h-24 bg-gray-200 rounded-full"></div>
      <div class="absolute top-1/2 left-1/4 w-12 h-12 lg:w-16 lg:h-16 bg-gray-200 rounded-full"></div>
    </div>
  </section>

  <!-- Horizontal Scroll Section - Mobile Friendly -->
  <section bind:this={horizontalScroll} class="relative bg-gray-50">
    <!-- Mobile Layout (Carousel) -->
    <div class="lg:hidden">
      <div class="relative overflow-hidden" on:touchstart={handleTouchStart} on:touchmove={handleTouchMove} on:touchend={handleTouchEnd}>
        <div 
          bind:this={mobileCarousel}
          class="flex transition-transform duration-500 ease-out"
          style="transform: translateX(-{currentSlide * 100}%)"
        >
          <!-- Section 1: About -->
          <div class="w-full flex-shrink-0 min-h-screen flex items-center justify-center p-4 sm:p-6 md:p-8 relative" style="background-image: url('https://res.cloudinary.com/dnnwvmh3n/image/upload/v1754776156/courtney-cook-h7aVq-7FfPw-unsplash_bhftmk.jpg'); background-size: cover; background-position: center; background-repeat: no-repeat;" aria-label="Professional web development workspace">
            <div class="max-w-2xl sm:max-w-3xl lg:max-w-4xl">
              <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl font-bold text-text mb-6 sm:mb-8 leading-tight">
                We specialize in professional web development and digital marketing services, creating interactive, high-performance websites that deliver exceptional user experiences and drive business growth.
              </h2>
              <p class="text-base sm:text-lg md:text-xl text-text/70 leading-relaxed">
                Our expertise in modern web technologies including React, Svelte, HTML5, CSS3, JavaScript, and Tailwind CSS, combined with comprehensive digital marketing strategies, positions us uniquely in the web development landscape.
              </p>
            </div>
          </div>
          
          <!-- Section 2: Services -->
          <div class="w-full flex-shrink-0 min-h-screen flex items-center justify-center p-4 sm:p-6 md:p-8 relative" style="background-image: url('https://res.cloudinary.com/dnnwvmh3n/image/upload/v1754776159/spacejoy-9M66C_w_ToM-unsplash_uwkjc2.jpg'); background-size: cover; background-position: center; background-repeat: no-repeat;" aria-label="Modern digital marketing and web services">
            <div class="max-w-4xl sm:max-w-5xl lg:max-w-6xl">
              <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl font-bold text-text mb-8 sm:mb-10 lg:mb-12 text-center leading-tight">
                Comprehensive Web Development & Digital Marketing Services
              </h2>
              <div class="grid grid-cols-1 md:grid-cols-2 gap-8 sm:gap-10 lg:gap-12">
                <div class="text-center">
                  <h3 class="text-xl sm:text-2xl font-bold text-text mb-3 sm:mb-4">Web Development</h3>
                  <p class="text-sm sm:text-base text-text/70 leading-relaxed">
                    Custom website development using React, Svelte, HTML5, CSS3, JavaScript (ES6+), and Tailwind CSS. We create responsive, fast-loading websites that provide exceptional user experiences and help improve search engine rankings.
                  </p>
                </div>
                <div class="text-center">
                  <h3 class="text-xl sm:text-2xl font-bold text-text mb-3 sm:mb-4">Digital Marketing</h3>
                  <p class="text-sm sm:text-base text-text/70 leading-relaxed">
                    Comprehensive digital marketing solutions including SEO optimization, Google Ads, Facebook Ads, Instagram Ads, TikTok Ads, and social media management to increase online presence and drive conversions.
                  </p>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Section 3: Contact -->
          <div class="w-full flex-shrink-0 min-h-screen flex items-center justify-center p-4 sm:p-6 md:p-8 relative" style="background-image: url('https://res.cloudinary.com/dnnwvmh3n/image/upload/v1754776161/jay-wennington-N_Y88TWmGwA-unsplash_wyxbbs.jpg'); background-size: cover; background-position: center; background-repeat: no-repeat;" aria-label="Business collaboration and project discussion">
            <div class="max-w-2xl sm:max-w-3xl lg:max-w-4xl text-center">
              <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl font-bold text-text mb-6 sm:mb-8 leading-tight">
                Let's work together
              </h2>
              <p class="text-base sm:text-lg md:text-xl text-text/70 mb-8 sm:mb-10 lg:mb-12 max-w-2xl mx-auto leading-relaxed">
                Ready to bring your vision to life? Let's discuss your project and create something amazing together.
              </p>
              <a href="/contact" class="btn-primary text-base sm:text-lg px-6 sm:px-8 py-3 sm:py-4 inline-block">
                Get in touch
              </a>
            </div>
          </div>
        </div>
        
        <!-- Navigation Dots -->
        <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2 flex space-x-3 z-10">
          {#each Array(3) as _, index}
            <button
              class="w-3 h-3 rounded-full transition-all duration-300 {currentSlide === index ? 'bg-white scale-125' : 'bg-white/50 hover:bg-white/75'}"
              on:click={() => goToSlide(index)}
              aria-label="Go to slide {index + 1}"
            ></button>
          {/each}
        </div>
        
        <!-- Navigation Arrows -->
        <button
          class="absolute left-4 top-1/2 transform -translate-y-1/2 w-12 h-12 bg-black/20 hover:bg-black/40 backdrop-blur-sm rounded-full flex items-center justify-center transition-all duration-300 z-10 {currentSlide === 0 ? 'opacity-50 cursor-not-allowed' : 'opacity-100 hover:scale-110'}"
          on:click={() => previousSlide()}
          disabled={currentSlide === 0}
          aria-label="Previous slide"
        >
          <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path>
          </svg>
        </button>
        
        <button
          class="absolute right-4 top-1/2 transform -translate-y-1/2 w-12 h-12 bg-black/20 hover:bg-black/40 backdrop-blur-sm rounded-full flex items-center justify-center transition-all duration-300 z-10 {currentSlide === 2 ? 'opacity-50 cursor-not-allowed' : 'opacity-100 hover:scale-110'}"
          on:click={() => nextSlide()}
          disabled={currentSlide === 2}
          aria-label="Next slide"
        >
          <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
          </svg>
        </button>
      </div>
    </div>
    
    <!-- Desktop Layout (Horizontal Scroll) -->
    <div class="hidden lg:flex w-max">
      <!-- Section 1: About -->
      <div class="w-screen h-screen flex items-center justify-center p-4 sm:p-6 md:p-8 relative" style="background-image: url('https://res.cloudinary.com/dnnwvmh3n/image/upload/v1754776156/courtney-cook-h7aVq-7FfPw-unsplash_bhftmk.jpg'); background-size: cover; background-position: center; background-repeat: no-repeat;" aria-label="Professional web development workspace">
        <div class="max-w-2xl sm:max-w-3xl lg:max-w-4xl">
          <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl font-bold text-text mb-6 sm:mb-8 leading-tight">
            We specialize in professional web development and digital marketing services, creating interactive, high-performance websites that deliver exceptional user experiences and drive business growth.
          </h2>
          <p class="text-base sm:text-lg md:text-xl text-text/70 leading-relaxed">
            Our expertise in modern web technologies including React, Svelte, HTML5, CSS3, JavaScript, and Tailwind CSS, combined with comprehensive digital marketing strategies, positions us uniquely in the web development landscape.
          </p>
        </div>
      </div>
      
      <!-- Section 2: Services -->
      <div class="w-screen h-screen flex items-center justify-center p-4 sm:p-6 md:p-8 relative" style="background-image: url('https://res.cloudinary.com/dnnwvmh3n/image/upload/v1754776159/spacejoy-9M66C_w_ToM-unsplash_uwkjc2.jpg'); background-size: cover; background-position: center; background-repeat: no-repeat;" aria-label="Modern digital marketing and web services">
        <div class="max-w-4xl sm:max-w-5xl lg:max-w-6xl">
          <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl font-bold text-text mb-8 sm:mb-10 lg:mb-12 text-center leading-tight">
            Comprehensive Web Development & Digital Marketing Services
          </h2>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-8 sm:gap-10 lg:gap-12">
            <div class="text-center">
              <h3 class="text-xl sm:text-2xl font-bold text-text mb-3 sm:mb-4">Web Development</h3>
              <p class="text-sm sm:text-base text-text/70 leading-relaxed">
                Custom website development using React, Svelte, HTML5, CSS3, JavaScript (ES6+), and Tailwind CSS. We create responsive, fast-loading websites that provide exceptional user experiences and help improve search engine rankings.
              </p>
            </div>
            <div class="text-center">
              <h3 class="text-xl sm:text-2xl font-bold text-text mb-3 sm:mb-4">Digital Marketing</h3>
              <p class="text-sm sm:text-base text-text/70 leading-relaxed">
                Comprehensive digital marketing solutions including SEO optimization, Google Ads, Facebook Ads, Instagram Ads, TikTok Ads, and social media management to increase online presence and drive conversions.
              </p>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Section 3: Contact -->
      <div class="w-screen h-screen flex items-center justify-center p-4 sm:p-6 md:p-8 relative" style="background-image: url('https://res.cloudinary.com/dnnwvmh3n/image/upload/v1754776161/jay-wennington-N_Y88TWmGwA-unsplash_wyxbbs.jpg'); background-size: cover; background-position: center; background-repeat: no-repeat;" aria-label="Business collaboration and project discussion">
        <div class="max-w-2xl sm:max-w-3xl lg:max-w-4xl text-center">
          <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl xl:text-6xl font-bold text-text mb-6 sm:mb-8 leading-tight">
            Let's work together
          </h2>
          <p class="text-base sm:text-lg md:text-xl text-text/70 mb-8 sm:mb-10 lg:mb-12 max-w-2xl mx-auto leading-relaxed">
            Ready to bring your vision to life? Let's discuss your project and create something amazing together.
          </p>
          <a href="/contact" class="btn-primary text-base sm:text-lg px-6 sm:px-8 py-3 sm:py-4 inline-block">
            Get in touch
          </a>
        </div>
      </div>
    </div>
  </section>

  <!-- Portfolio Showcase Section -->
  <section class="section-padding bg-white overflow-hidden">
    <div class="container-custom">
      <!-- Portfolio Grid - Responsive and Touch-Friendly -->
      <div class="portfolio-container">
        <!-- Portfolio Item 1 -->
        <div class="portfolio-card">
          <div class="portfolio-image-container">
            <img 
              src="https://res.cloudinary.com/dnnwvmh3n/image/upload/v1754776156/courtney-cook-h7aVq-7FfPw-unsplash_bhftmk.jpg" 
              alt="Modern Business Website Design"
              class="portfolio-image"
              loading="lazy"
            />
          </div>
        </div>
        
        <!-- Portfolio Item 2 -->
        <div class="portfolio-card">
          <div class="portfolio-image-container">
            <img 
              src="https://res.cloudinary.com/dnnwvmh3n/image/upload/v1754776159/spacejoy-9M66C_w_ToM-unsplash_uwkjc2.jpg" 
              alt="E-commerce Website Development"
              class="portfolio-image"
              loading="lazy"
            />
          </div>
        </div>
        
        <!-- Portfolio Item 3 -->
        <div class="portfolio-card">
          <div class="portfolio-image-container">
            <img 
              src="https://res.cloudinary.com/dnnwvmh3n/image/upload/v1754776161/jay-wennington-N_Y88TWmGwA-unsplash_wyxbbs.jpg" 
              alt="Digital Marketing Campaign Results"
              class="portfolio-image"
              loading="lazy"
            />
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Featured Services Preview Section -->
  <section class="section-padding bg-white">
    <div class="container-custom">
      <div class="text-center mb-12 sm:mb-16">
        <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
          Featured Services
        </h2>
        <p class="text-lg sm:text-xl text-text/70 max-w-2xl mx-auto leading-relaxed">
          Discover how we can help your business grow online
        </p>
      </div>
      
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 sm:gap-8">
        <!-- Service Card 1: Modern Web Design -->
        <div class="bg-primary p-6 sm:p-8 rounded-2xl card-shadow hover:-translate-y-2 transition-all duration-300">
          <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
            <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
            </svg>
          </div>
          <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">Modern Web Design</h3>
          <p class="text-sm sm:text-base text-text/70 leading-relaxed mb-4 sm:mb-6">
            We create websites that combine style with performance. Our designs are mobile-friendly, fast-loading, and tailored to your brand identity.
          </p>
          <a href="/websites" class="text-secondary font-semibold hover:text-text transition-colors text-sm sm:text-base">
            Learn More →
          </a>
        </div>
        
        <!-- Service Card 2: Digital Marketing -->
        <div class="bg-primary p-6 sm:p-8 rounded-2xl card-shadow hover:-translate-y-2 transition-all duration-300">
          <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
            <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
            </svg>
          </div>
          <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">Digital Marketing</h3>
          <p class="text-sm sm:text-base text-text/70 leading-relaxed mb-4 sm:mb-6">
            From SEO to social media marketing, we help you get found online and connect with the right audience.
          </p>
          <a href="/websites" class="text-secondary font-semibold hover:text-text transition-colors text-sm sm:text-base">
            Learn More →
          </a>
        </div>
        
        <!-- Service Card 3: Business Profiles -->
        <div class="bg-primary p-6 sm:p-8 rounded-2xl card-shadow hover:-translate-y-2 transition-all duration-300 sm:col-span-2 lg:col-span-1">
          <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
            <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" />
            </svg>
          </div>
          <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">Business Profiles</h3>
          <p class="text-sm sm:text-base text-text/70 leading-relaxed mb-4 sm:mb-6">
            We design professional online business profiles that present your company in the best light, building trust with your audience.
          </p>
          <a href="/websites" class="text-secondary font-semibold hover:text-text transition-colors text-sm sm:text-base">
            Learn More →
          </a>
        </div>
      </div>
    </div>
  </section>

  <!-- About Section -->
  <section bind:this={sections} class="section-padding bg-gray-50">
    <div class="container-custom">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 sm:gap-16 items-center">
        <!-- About Text -->
        <div>
          <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-6 sm:mb-8 leading-tight">
            We are not just web developers
          </h2>
          <p class="text-base sm:text-lg text-text/70 mb-6 sm:mb-8 leading-relaxed">
            LunexWeb does web development and digital marketing. We create comprehensive digital solutions that help businesses thrive in the online world.
          </p>
          
          <!-- Skills -->
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 sm:gap-6">
            <div class="text-center p-3 sm:p-4 bg-gray-100 rounded-lg subtle-border">
              <div class="w-10 h-10 sm:w-12 sm:h-12 bg-gray-200 rounded-lg mx-auto mb-2 sm:mb-3 flex items-center justify-center">
                <svg class="w-5 h-5 sm:w-6 sm:h-6 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                </svg>
              </div>
              <h4 class="font-semibold text-black text-sm sm:text-base">Web Development</h4>
            </div>
            
            <div class="text-center p-3 sm:p-4 bg-gray-100 rounded-lg subtle-border">
              <div class="w-10 h-10 sm:w-12 sm:h-12 bg-gray-200 rounded-lg mx-auto mb-2 sm:mb-3 flex items-center justify-center">
                <svg class="w-5 h-5 sm:w-6 sm:h-6 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
                </svg>
              </div>
              <h4 class="font-semibold text-black text-sm sm:text-base">Digital Marketing</h4>
            </div>
            
            <div class="text-center p-3 sm:p-4 bg-gray-100 rounded-lg subtle-border">
              <div class="w-10 h-10 sm:w-12 sm:h-12 bg-gray-200 rounded-lg mx-auto mb-2 sm:mb-3 flex items-center justify-center">
                <svg class="w-5 h-5 sm:w-6 sm:h-6 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z" />
                </svg>
              </div>
              <h4 class="font-semibold text-black text-sm sm:text-base">Strategy</h4>
            </div>
          </div>
        </div>
        
        <!-- About Video -->
        <div>
          <div class="relative">
            <div class="w-full h-64 sm:h-80 md:h-96 bg-gray-200 rounded-2xl overflow-hidden">
              <video 
                class="w-full h-full object-cover rounded-2xl"
                autoplay 
                muted 
                loop 
                playsinline
                preload="metadata"
              >
                <source src="https://res.cloudinary.com/dnnwvmh3n/video/upload/v1754852722/desktop_au8jqy.mp4" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            </div>
            <div class="absolute -bottom-2 sm:-bottom-4 -right-2 sm:-right-4 w-20 h-20 sm:w-32 sm:h-32 bg-black rounded-2xl opacity-10"></div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Services Section -->
  <section bind:this={sections} class="section-padding bg-white">
    <div class="container-custom">
      <div class="text-center mb-12 sm:mb-16">
        <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
          Our Services
        </h2>
        <p class="text-lg sm:text-xl text-text/70 max-w-2xl mx-auto leading-relaxed">
          Comprehensive digital solutions to help your business grow
        </p>
      </div>
      
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6 sm:gap-8">
        <!-- Service Card 1 -->
        <div class="bg-primary p-6 sm:p-8 rounded-2xl card-shadow hover:-translate-y-2 transition-all duration-300">
          <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
            <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
            </svg>
          </div>
          <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">Web Development</h3>
          <p class="text-sm sm:text-base text-text/70 leading-relaxed">
            Custom websites built with React, Svelte, HTML5, CSS3, JavaScript, and Tailwind CSS for optimal performance, user experience, and search engine rankings.
          </p>
        </div>
        
        <!-- Service Card 2 -->
        <div class="bg-primary p-6 sm:p-8 rounded-2xl card-shadow hover:-translate-y-2 transition-all duration-300">
          <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
            <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
            </svg>
          </div>
          <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">Digital Marketing</h3>
          <p class="text-sm sm:text-base text-text/70 leading-relaxed">
            Comprehensive digital marketing including SEO optimization, Google Ads, Facebook Ads, Instagram Ads, TikTok Ads, and social media management to increase online presence and drive conversions.
          </p>
        </div>
        
        <!-- Service Card 3 -->
        <div class="bg-primary p-6 sm:p-8 rounded-2xl card-shadow hover:-translate-y-2 transition-all duration-300">
          <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
            <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
            </svg>
          </div>
          <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">SEO Optimization</h3>
          <p class="text-sm sm:text-base text-text/70 leading-relaxed">
            Search engine optimization to improve your website's visibility and rankings.
          </p>
        </div>
        
        <!-- Service Card 4 -->
        <div class="bg-primary p-6 sm:p-8 rounded-2xl card-shadow hover:-translate-y-2 transition-all duration-300">
          <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
            <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
            </svg>
          </div>
          <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">Analytics & Reporting</h3>
          <p class="text-sm sm:text-base text-text/70 leading-relaxed">
            Data-driven insights to track performance and optimize your digital strategy.
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- Contact Section -->
  <section bind:this={sections} class="section-padding bg-primary">
    <div class="container-custom">
      <div class="max-w-4xl mx-auto text-center">
        <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
          Let's Work Together
        </h2>
        <p class="text-lg sm:text-xl text-text/70 mb-8 sm:mb-10 lg:mb-12 max-w-2xl mx-auto leading-relaxed">
          Ready to bring your vision to life? Let's discuss your project and create something amazing together.
        </p>
        
        <!-- Contact Information -->
        <div class="bg-secondary/20 rounded-2xl p-6 sm:p-8 max-w-2xl mx-auto">
          <h3 class="text-xl sm:text-2xl font-bold text-text mb-4 sm:mb-6">Get In Touch</h3>
          
          <!-- Email Contacts -->
          <div class="space-y-3 sm:space-y-4 mb-4 sm:mb-6">
            <div class="flex items-center justify-center gap-2 sm:gap-3">
              <svg class="w-5 h-5 sm:w-6 sm:h-6 text-text" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
              </svg>
              <a href="mailto:inquiry@lunexweb.com" class="text-base sm:text-lg text-text hover:text-blue-600 transition-colors font-medium">
                inquiry@lunexweb.com
              </a>
            </div>
            
            <div class="flex items-center justify-center gap-2 sm:gap-3">
              <svg class="w-5 h-5 sm:w-6 sm:h-6 text-text" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
              </svg>
              <a href="mailto:hello@lunexweb.com" class="text-base sm:text-lg text-text hover:text-blue-600 transition-colors font-medium">
                hello@lunexweb.com
              </a>
            </div>
          </div>
          
          <!-- Instagram Contact -->
          <div class="flex items-center justify-center gap-2 sm:gap-3 mb-4 sm:mb-6">
            <svg class="w-5 h-5 sm:w-6 sm:h-6 text-text" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12.017 0C5.396 0 .029 5.367.029 11.987c0 5.079 3.158 9.417 7.618 11.174-.105-.949-.199-2.403.041-3.439.219-.937 1.406-5.957 1.406-5.957s-.359-.72-.359-1.781c0-1.663.967-2.911 2.168-2.911 1.024 0 1.518.769 1.518 1.688 0 1.029-.653 2.567-.992 3.992-.285 1.193.6 2.165 1.775 2.165 2.128 0 3.768-2.245 3.768-5.487 0-2.861-2.063-4.869-5.008-4.869-3.41 0-5.409 2.562-5.409 5.199 0 1.033.394 2.143.889 2.741.099.12.112.225.085.345-.09.375-.292 1.199-.334 1.363-.053.225-.172.271-.402.165-1.495-.69-2.433-2.878-2.433-4.646 0-3.776 2.748-7.252 7.92-7.252 4.158 0 7.392 2.967 7.392 6.923 0 4.135-2.607 7.462-6.233 7.462-1.214 0-2.357-.629-2.746-1.378l-.748 2.853c-.271 1.043-1.002 2.35-1.492 3.146C9.57 23.812 10.763 24.009 12.017 24.009c6.624 0 11.99-5.367 11.99-11.988C24.007 5.367 18.641.001 12.017.001z"/>
            </svg>
            <span class="text-base sm:text-lg text-text font-medium">Follow us on Instagram</span>
          </div>
          
          <!-- Video Call Availability -->
          <div class="bg-blue-50 rounded-lg p-3 sm:p-4 border border-blue-200">
            <p class="text-blue-800 text-xs sm:text-sm">
              <strong>Available for video calls:</strong> Zoom and Microsoft Teams
            </p>
          </div>
          
          <!-- Contact Buttons -->
          <div class="flex flex-col sm:flex-row items-center justify-center gap-3 sm:gap-4 mt-4 sm:mt-6">
            <a href="mailto:inquiry@lunexweb.com" class="btn-secondary px-6 sm:px-8 py-2.5 sm:py-3 w-full sm:w-auto">
              Send Inquiry
            </a>
            <a href="mailto:hello@lunexweb.com" class="btn-primary px-6 sm:px-8 py-2.5 sm:py-3 w-full sm:w-auto">
              Say Hello
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</div> 