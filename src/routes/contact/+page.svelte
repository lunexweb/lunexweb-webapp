<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  
  gsap.registerPlugin(ScrollTrigger);
  
  let contactSection;
  let contactInfo;
  
  onMount(() => {
    // Contact section animation
    gsap.fromTo(contactSection, 
      { opacity: 0, y: 50 },
      { 
        opacity: 1, 
        y: 0, 
        duration: 1, 
        ease: "power3.out",
        scrollTrigger: {
          trigger: contactSection,
          start: "top 80%",
          end: "bottom 20%",
          toggleActions: "play none none reverse"
        }
      }
    );
    
    // Contact info animation
    gsap.fromTo(contactInfo, 
      { opacity: 0, x: -50 },
      { 
        opacity: 1, 
        x: 0, 
        duration: 1, 
        ease: "power3.out",
        delay: 0.3,
        scrollTrigger: {
          trigger: contactInfo,
          start: "top 80%",
          end: "bottom 20%",
          toggleActions: "play none none reverse"
        }
      }
    );
  });
</script>

<svelte:head>
  <title>Contact Us - LunexWeb | Professional Web Development & Digital Marketing</title>
  <meta name="description" content="Get in touch with LunexWeb for professional web development and digital marketing services in Johannesburg, South Africa. Let's discuss your project today." />
</svelte:head>

<!-- Hero Section with Background Image -->
<section class="relative min-h-screen flex items-center justify-center overflow-hidden">
  <!-- Background Image -->
  <div class="absolute inset-0 z-0">
    <img 
      src="https://res.cloudinary.com/dnnwvmh3n/image/upload/v1754771046/maciej-drazkiewicz-XORfEIs_LTk-unsplash_anl9b7.jpg" 
      alt="Modern office workspace" 
      class="w-full h-full object-cover"
    />
    <!-- Overlay for better text readability -->
    <div class="absolute inset-0 bg-black/50"></div>
  </div>
  
  <!-- Content -->
  <div class="relative z-10 container-custom px-4 text-center text-white">
    <h1 class="text-4xl sm:text-5xl md:text-6xl lg:text-7xl font-bold mb-6 sm:mb-8 leading-tight">
      Let's Build Something
      <span class="text-primary">Amazing</span>
    </h1>
    <p class="text-lg sm:text-xl md:text-2xl text-gray-200 max-w-3xl mx-auto mb-8 sm:mb-12 leading-relaxed">
      Ready to transform your business with cutting-edge web development and digital marketing? 
      Let's discuss your vision and make it a reality.
    </p>
    <div class="flex flex-col sm:flex-row gap-4 sm:gap-6 justify-center">
      <a href="mailto:info@lunexweb.com" class="bg-primary text-text px-8 py-4 rounded-xl font-semibold text-lg hover:bg-opacity-90 transition-all duration-300 hover:scale-105">
        Send Email
      </a>
      <a href="mailto:support@lunexweb.com" class="bg-text text-primary px-8 py-4 rounded-xl font-semibold text-lg hover:bg-opacity-90 transition-all duration-300 hover:scale-105">
        Support Email
      </a>
    </div>
  </div>
</section>

<!-- Contact Information Section -->
<section bind:this={contactSection} class="section-padding bg-primary">
  <div class="container-custom">
    <div class="text-center mb-16">
      <h2 class="text-3xl sm:text-4xl md:text-5xl font-bold text-text mb-6 leading-tight">
        Get In Touch
      </h2>
      <p class="text-lg sm:text-xl text-text/70 max-w-2xl mx-auto leading-relaxed">
        We're here to help bring your digital vision to life. Reach out through any of these channels.
      </p>
    </div>
    
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8 sm:gap-12 max-w-4xl mx-auto">
      <!-- Primary Email Contact -->
      <div bind:this={contactInfo} class="bg-white p-8 rounded-2xl card-shadow hover:-translate-y-2 transition-all duration-300 text-center">
        <div class="w-16 h-16 bg-primary rounded-2xl mb-6 mx-auto flex items-center justify-center">
          <svg class="w-8 h-8 text-text" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
          </svg>
        </div>
        <h3 class="text-xl font-bold text-text mb-4">Primary Contact</h3>
        <p class="text-text/70 mb-4">For general inquiries and project discussions</p>
        <a href="mailto:info@lunexweb.com" class="text-primary font-semibold hover:underline text-lg">
          info@lunexweb.com
        </a>
      </div>
      
      <!-- Secondary Email Contact -->
      <div class="bg-white p-8 rounded-2xl card-shadow hover:-translate-y-2 transition-all duration-300 text-center">
        <div class="w-16 h-16 bg-primary rounded-2xl mb-6 mx-auto flex items-center justify-center">
          <svg class="w-8 h-8 text-text" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
          </svg>
        </div>
        <h3 class="text-xl font-bold text-text mb-4">Support Contact</h3>
        <p class="text-text/70 mb-4">For technical support and urgent matters</p>
        <a href="mailto:support@lunexweb.com" class="text-primary font-semibold hover:underline text-lg">
          support@lunexweb.com
        </a>
      </div>
    </div>
  </div>
</section>

<!-- Social Media & Location Section -->
<section class="section-padding bg-gray-50">
  <div class="container-custom">
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
      <!-- Social Media -->
      <div>
        <h3 class="text-2xl sm:text-3xl font-bold text-text mb-6">Connect With Us</h3>
        <p class="text-lg text-text/70 mb-8 leading-relaxed">
          Follow us on Instagram to see our latest work, industry insights, and behind-the-scenes content.
        </p>
        <div class="flex justify-center">
          <a href="https://www.instagram.com/lunexweb?igsh=ZzE2OGhkNDk5d2p6" target="_blank" rel="noopener noreferrer" class="bg-primary p-6 rounded-2xl hover:bg-opacity-90 transition-all duration-300 hover:scale-110">
            <svg class="w-8 h-8 text-text" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
            </svg>
          </a>
        </div>
      </div>
      
      <!-- Location -->
      <div class="bg-white p-8 rounded-2xl card-shadow">
        <h3 class="text-2xl sm:text-3xl font-bold text-text mb-6">Our Location</h3>
        <div class="flex items-start space-x-4 mb-6">
          <div class="w-12 h-12 bg-primary rounded-xl flex items-center justify-center flex-shrink-0">
            <svg class="w-6 h-6 text-text" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
            </svg>
          </div>
          <div>
            <h4 class="text-lg font-semibold text-text mb-2">Johannesburg, South Africa</h4>
            <p class="text-text/70">Serving clients across South Africa and internationally</p>
          </div>
        </div>
        <div class="flex items-start space-x-4">
          <div class="w-12 h-12 bg-primary rounded-xl flex items-center justify-center flex-shrink-0">
            <svg class="w-6 h-6 text-text" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
          </div>
          <div>
            <h4 class="text-lg font-semibold text-text mb-2">Business Hours</h4>
            <p class="text-text/70">Monday - Friday: 8:00 AM - 6:00 PM<br>Weekends and Public Holidays: Closed</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- CTA Section -->
<section class="section-padding bg-text">
  <div class="container-custom text-center">
    <h2 class="text-3xl sm:text-4xl md:text-5xl font-bold text-white mb-6 leading-tight">
      Ready to Start Your Project?
    </h2>
    <p class="text-lg sm:text-xl text-gray-200 max-w-2xl mx-auto mb-8 leading-relaxed">
      Let's discuss how we can help transform your business with cutting-edge web solutions and digital marketing strategies.
    </p>
    <div class="flex flex-col sm:flex-row gap-4 justify-center">
      <a href="mailto:info@lunexweb.com" class="bg-primary text-text px-8 py-4 rounded-xl font-semibold text-lg hover:bg-opacity-90 transition-all duration-300 hover:scale-105">
        Get Started Today
      </a>
      <a href="/packages" class="border-2 border-white text-white px-8 py-4 rounded-xl font-semibold text-lg hover:bg-white hover:text-text transition-all duration-300">
        View Packages
      </a>
    </div>
  </div>
</section> 