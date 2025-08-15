<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  
  gsap.registerPlugin(ScrollTrigger);
  
  let packagesSection;
  let heroSection;
  let businessSection;
  
  onMount(() => {
    // Hero text animation
    if (heroSection) {
      gsap.fromTo(heroSection.querySelector('.hero-title'), 
        { opacity: 0, y: 100 },
        { 
          opacity: 1, 
          y: 0, 
          duration: 1.2, 
          ease: "power3.out",
          delay: 0.3
        }
      );
      
      gsap.fromTo(heroSection.querySelector('.hero-subtitle'), 
        { opacity: 0, y: 50 },
        { 
          opacity: 1, 
          y: 0, 
          duration: 1, 
          ease: "power3.out",
          delay: 0.6
        }
      );
    }
    
    // Business understanding section animation
    if (businessSection) {
      gsap.fromTo(businessSection.querySelectorAll('.business-card'), 
        { opacity: 0, y: 60, scale: 0.95 },
        { 
          opacity: 1, 
          y: 0, 
          scale: 1,
          duration: 1, 
          ease: "power3.out",
          stagger: 0.3,
          scrollTrigger: {
            trigger: businessSection,
            start: "top 80%",
            toggleActions: "play none none none"
          }
        }
      );
    }
    
    // Animate packages on scroll
    if (packagesSection) {
      gsap.fromTo(packagesSection.querySelectorAll('.package-card'), 
        { opacity: 0, y: 80, scale: 0.95 },
        { 
          opacity: 1, 
          y: 0, 
          scale: 1,
          duration: 1, 
          ease: "power3.out",
          stagger: 0.2,
          scrollTrigger: {
            trigger: packagesSection,
            start: "top 80%",
            toggleActions: "play none none none"
          }
        }
      );
    }
  });
</script>

<svelte:head>
  <title>Our Packages - LunexWeb | Web Development & Digital Marketing Services in Johannesburg</title>
  <meta name="description" content="Choose from our professional web development and digital marketing packages. Premium solutions at competitive prices to help your business thrive online in Johannesburg, South Africa." />
  <meta name="keywords" content="web development packages Johannesburg, digital marketing packages South Africa, website pricing, SEO packages, Google Ads packages, social media packages" />
</svelte:head>

<!-- Hero Section with Background Image -->
<section bind:this={heroSection} class="min-h-screen flex items-center justify-center relative overflow-hidden">
  <!-- Background Image with Parallax Effect -->
  <div class="absolute inset-0 z-0">
    <img 
      src="https://res.cloudinary.com/dnnwvmh3n/image/upload/v1754771035/kenan-kitchen-NuVatYA1cEU-unsplash_ldr8ed.jpg" 
      alt="Professional business environment representing our premium web development and digital marketing packages" 
      class="w-full h-full object-cover scale-110"
    />
    <!-- Enhanced overlay for better text readability -->
    <div class="absolute inset-0 bg-gradient-to-b from-black/60 via-black/40 to-black/70"></div>
    <!-- Subtle pattern overlay -->
    <div class="absolute inset-0 opacity-10" style="background-image: url('data:image/svg+xml,%3Csvg%20width%3D%2260%22%20height%3D%2260%22%20viewBox%3D%220%200%2060%2060%22%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%3E%3Cg%20fill%3D%22none%22%20fill-rule%3D%22evenodd%22%3E%3Cg%20fill%3D%22%23ffffff%22%20fill-opacity%3D%220.1%22%3E%3Ccircle%20cx%3D%2230%22%20cy%3D%2230%22%20r%3D%221%22/%3E%3C/g%3E%3C/g%3E%3C/svg%3E');"></div>
  </div>
  
  <div class="container-custom text-center px-4 relative z-10">
    <div class="max-w-4xl sm:max-w-5xl mx-auto">
      <h1 class="hero-title text-4xl sm:text-5xl md:text-6xl lg:text-7xl xl:text-8xl 2xl:text-9xl font-black text-white mb-6 sm:mb-8 leading-none tracking-tight">
        Our Packages
      </h1>
      <p class="hero-subtitle text-lg sm:text-xl md:text-2xl lg:text-3xl xl:text-4xl text-white/95 mb-12 sm:mb-16 max-w-3xl sm:max-w-4xl mx-auto leading-relaxed font-light">
        We don't just charge - we first understand your business and your customers to help you bring real ROI because we understand your investment
      </p>
      
      <!-- Floating action button -->
      <div class="animate-bounce">
        <a href="#business-first" class="inline-flex items-center gap-2 sm:gap-3 bg-white/20 backdrop-blur-sm text-white px-6 sm:px-8 py-3 sm:py-4 rounded-full border border-white/30 hover:bg-white/30 transition-all duration-300 group text-sm sm:text-lg">
          <span class="font-medium">Discover Our Approach</span>
          <svg class="w-5 h-5 sm:w-6 sm:h-6 group-hover:translate-x-1 transition-transform duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
          </svg>
        </a>
      </div>
    </div>
  </div>
  
  <!-- Floating decorative elements -->
  <div class="absolute inset-0 pointer-events-none">
    <div class="absolute top-20 left-10 w-2 h-2 bg-white/30 rounded-full animate-pulse"></div>
    <div class="absolute top-32 right-20 w-1 h-1 bg-white/40 rounded-full animate-ping"></div>
    <div class="absolute bottom-32 left-1/4 w-1.5 h-1.5 bg-white/25 rounded-full animate-bounce"></div>
  </div>
</section>

<!-- Business-First Approach Section -->
<section id="business-first" bind:this={businessSection} class="section-padding bg-gradient-to-br from-blue-50 via-white to-indigo-50">
  <div class="container-custom">
    <div class="text-center mb-12 sm:mb-16">
      <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
        Understanding Before Pricing
      </h2>
      <p class="text-lg sm:text-xl text-text/70 max-w-4xl mx-auto leading-relaxed">
        Our packages are delivered based on your specific needs and budget. Whether you want a website only, 
        digital marketing only, or both, we'll customize the solution to fit your requirements and deliver 
        maximum value for your investment.
      </p>
    </div>
    
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 sm:gap-8 mb-12">
      <div class="business-card bg-white p-6 sm:p-8 rounded-2xl shadow-lg hover:shadow-xl transition-all duration-300 border-l-4 border-blue-500">
        <div class="text-center mb-4">
          <div class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mx-auto mb-4">
            <svg class="w-8 h-8 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
          </div>
          <h3 class="text-xl font-bold text-text mb-2">Business Analysis</h3>
          <p class="text-text/70 text-sm">We analyze your business model, target audience, and competitive landscape to understand your unique position in the market.</p>
        </div>
      </div>
      
      <div class="business-card bg-white p-6 sm:p-8 rounded-2xl shadow-lg hover:shadow-xl transition-all duration-300 border-l-4 border-green-500">
        <div class="text-center mb-4">
          <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
            <svg class="w-8 h-8 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z" />
            </svg>
          </div>
          <h3 class="text-xl font-bold text-text mb-2">Customer Insights</h3>
          <p class="text-text/70 text-sm">We dive deep into understanding your customers' needs, pain points, and behavior patterns to create solutions that truly resonate.</p>
        </div>
      </div>
      
      <div class="business-card bg-white p-6 sm:p-8 rounded-2xl shadow-lg hover:shadow-xl transition-all duration-300 border-l-4 border-gray-500">
        <div class="text-center mb-4">
          <div class="w-16 h-16 bg-gray-100 rounded-full flex items-center justify-center mx-auto mb-4">
            <svg class="w-8 h-8 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6" />
            </svg>
          </div>
          <h3 class="text-xl font-bold text-text mb-2">ROI Focus</h3>
          <p class="text-text/70 text-sm">Every solution we create is designed with your return on investment in mind, ensuring your budget delivers measurable business results.</p>
        </div>
      </div>
    </div>
    
    <div class="bg-gradient-to-r from-blue-600 to-gray-600 rounded-3xl p-8 sm:p-12 text-center text-white">
      <h3 class="text-2xl sm:text-3xl font-bold mb-4">Ready to Get Started?</h3>
      <p class="text-lg text-blue-100 mb-6 max-w-2xl mx-auto">
        Let's have a conversation about your business goals. We'll help you choose the right package based on your needs and budget.
      </p>
      <a href="/contact" class="inline-flex items-center gap-2 bg-white text-blue-600 px-8 py-4 rounded-full font-semibold hover:bg-blue-50 transition-all duration-300">
        <span>Schedule a Consultation</span>
        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
        </svg>
      </a>
    </div>
  </div>
</section>

<!-- Packages Section -->
<section id="packages" bind:this={packagesSection} class="section-padding bg-white">
  <div class="container-custom">
    <div class="text-center mb-12 sm:mb-16">
      <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
        Flexible Package Options
      </h2>
      <p class="text-lg sm:text-xl text-text/70 max-w-3xl mx-auto leading-relaxed">
        Our packages are delivered based on your specific needs and budget. Whether you need a website only, 
        digital marketing only, or both, we'll customize the solution to fit your requirements.
      </p>
    </div>
    
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 sm:gap-8">
      <!-- Starter Package -->
      <div class="package-card bg-gradient-to-br from-gray-50 to-white p-6 sm:p-8 rounded-2xl shadow-lg hover:shadow-xl transition-all duration-300 border border-gray-100">
        <div class="text-center mb-6 sm:mb-8">
          <div class="w-20 h-20 bg-blue-100 rounded-full flex items-center justify-center mx-auto mb-4">
            <svg class="w-10 h-10 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
            </svg>
          </div>
          <h3 class="text-xl sm:text-2xl font-bold text-text mb-3">Starter</h3>
          <div class="text-3xl sm:text-4xl font-bold text-text mb-2">
            $499 - $1,999
          </div>
          <p class="text-sm sm:text-base text-text/70">Perfect for small businesses getting started online</p>
        </div>
        
        <div class="text-center">
          <p class="text-text/80 text-sm leading-relaxed">
            Ideal for businesses looking to establish their online presence with essential web development 
            or digital marketing services tailored to their specific needs and budget constraints.
          </p>
        </div>
      </div>
      
      <!-- Professional Package -->
      <div class="package-card bg-gradient-to-br from-blue-600 to-blue-700 text-white p-6 sm:p-8 rounded-2xl shadow-xl hover:shadow-xl transition-all duration-300 relative">
        
        <div class="text-center mb-6 sm:mb-8">
          <div class="w-20 h-20 bg-white/20 rounded-full flex items-center justify-center mx-auto mb-4">
            <svg class="w-10 h-10 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
            </svg>
          </div>
          <h3 class="text-xl sm:text-2xl font-bold mb-3">Professional</h3>
          <div class="text-3xl sm:text-4xl font-bold mb-2">
            $2,000 - $5,999
          </div>
          <p class="text-blue-100">Comprehensive solution for growing businesses</p>
        </div>
        
        <div class="text-center">
          <p class="text-blue-100 text-sm leading-relaxed">
            Perfect for established businesses seeking advanced web development features, comprehensive 
            digital marketing strategies, or integrated solutions that drive growth and engagement.
          </p>
        </div>
      </div>
      
      <!-- Enterprise Package -->
      <div class="package-card bg-gradient-to-br from-gray-800 to-gray-900 text-white p-6 sm:p-8 rounded-2xl shadow-lg hover:shadow-xl transition-all duration-300">
        <div class="text-center mb-6 sm:mb-8">
          <div class="w-20 h-20 bg-gray-700 rounded-full flex items-center justify-center mx-auto mb-4">
            <svg class="w-10 h-10 text-gray-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" />
            </svg>
          </div>
          <h3 class="text-xl sm:text-2xl font-bold mb-3">Enterprise</h3>
          <div class="text-3xl sm:text-4xl font-bold mb-2">
            $6,000 - $12,000
          </div>
          <p class="text-gray-300">Full-featured solution for established businesses</p>
        </div>
        
        <div class="text-center">
          <p class="text-gray-300 text-sm leading-relaxed">
            Designed for large businesses requiring enterprise-level web solutions, advanced digital 
            marketing campaigns, or comprehensive digital transformation services with premium support.
          </p>
        </div>
      </div>
    </div>
    
    <div class="text-center mt-12">
      <p class="text-text/70 text-lg max-w-3xl mx-auto">
        <strong>Note:</strong> Package contents are customized based on your specific requirements. 
        We'll work with you to determine the exact services and features that fit within your chosen budget range.
      </p>
      <p class="text-text/60 text-base mt-4 font-semibold">
        All prices are in US Dollars ($)
      </p>
    </div>
  </div>
</section>

<!-- Service Categories Section -->
<section class="section-padding bg-gradient-to-br from-gray-50 to-blue-50">
  <div class="container-custom">
    <div class="text-center mb-12 sm:mb-16">
      <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
        What We Deliver
      </h2>
      <p class="text-lg sm:text-xl text-text/70 max-w-3xl mx-auto leading-relaxed">
        Based on your package selection, we can deliver any combination of these services to meet your business needs.
      </p>
    </div>
    
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8 sm:gap-12">
      <!-- Web Development -->
      <div class="bg-white p-8 rounded-2xl shadow-lg hover:shadow-xl transition-all duration-300">
        <div class="flex items-center gap-4 mb-6">
          <div class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center">
            <svg class="w-8 h-8 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
            </svg>
          </div>
          <h3 class="text-2xl font-bold text-text">Web Development</h3>
        </div>
        <p class="text-text/70 leading-relaxed mb-4">
          From simple landing pages to complex e-commerce platforms, we build websites that convert visitors into customers.
        </p>
        <ul class="space-y-2 text-sm text-text/70">
          <li>• Responsive design for all devices</li>
          <li>• SEO-optimized structure</li>
          <li>• Fast loading performance</li>
          <li>• Content management systems</li>
          <li>• E-commerce functionality</li>
        </ul>
      </div>
      
      <!-- Digital Marketing -->
      <div class="bg-white p-8 rounded-2xl shadow-lg hover:shadow-xl transition-all duration-300">
        <div class="flex items-center gap-4 mb-6">
          <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center">
            <svg class="w-8 h-8 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 8v8m-4-5v5m-4-2v2m-2 4h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />
            </svg>
          </div>
          <h3 class="text-2xl font-bold text-text">Digital Marketing</h3>
        </div>
        <p class="text-text/70 leading-relaxed mb-4">
          Strategic marketing campaigns that drive traffic, generate leads, and increase your online visibility.
        </p>
        <ul class="space-y-2 text-sm text-text/70">
          <li>• Search Engine Optimization (SEO)</li>
          <li>• Google Ads & PPC campaigns</li>
          <li>• Social media marketing</li>
          <li>• Content marketing strategies</li>
          <li>• Analytics & performance tracking</li>
        </ul>
      </div>
    </div>
  </div>
</section>

<!-- CTA Section -->
<section class="section-padding bg-gray-100">
  <div class="container-custom text-center">
    <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-gray-800 mb-4 sm:mb-6 leading-tight">
      Ready to Transform Your Business?
    </h2>
    <p class="text-lg sm:text-xl text-gray-600 mb-8 sm:mb-10 max-w-3xl mx-auto leading-relaxed">
      Let's discuss your business goals and find the perfect package that fits your needs and budget. 
      Our consultation is free, and we'll help you make an informed decision.
    </p>
    <div class="flex items-center justify-center">
      <a href="/contact" class="bg-blue-600 text-white px-8 py-4 rounded-full font-semibold hover:bg-blue-700 transition-all duration-300 text-lg">
        Schedule Free Consultation
      </a>
    </div>
  </div>
</section> 