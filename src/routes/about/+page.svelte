<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  
  gsap.registerPlugin(ScrollTrigger);
  
  let aboutContent;
  let skillsSection;
  let experienceSection;
  
  onMount(() => {
    // About content animation
    gsap.fromTo(aboutContent, 
      { opacity: 0, y: 30 },
      { 
        opacity: 1, 
        y: 0, 
        duration: 1, 
        ease: "power3.out",
        delay: 0.3
      }
    );
    
    // Skills section animation
    gsap.fromTo(skillsSection.querySelectorAll('.skill-item'), 
      { opacity: 0, y: 20 },
      { 
        opacity: 1, 
        y: 0, 
        duration: 0.8, 
        ease: "power3.out",
        stagger: 0.1,
        scrollTrigger: {
          trigger: skillsSection,
          start: "top 80%",
          end: "bottom 20%",
          toggleActions: "play none none reverse"
        }
      }
    );
    
    // Experience section animation
    gsap.fromTo(experienceSection.querySelectorAll('.experience-item'), 
      { opacity: 0, x: -30 },
      { 
        opacity: 1, 
        x: 0, 
        duration: 0.8, 
        ease: "power3.out",
        stagger: 0.2,
        scrollTrigger: {
          trigger: experienceSection,
          start: "top 80%",
          end: "bottom 20%",
          toggleActions: "play none none reverse"
        }
      }
    );
  });
</script>

<svelte:head>
  <title>About LunexWeb - Web Development & Digital Marketing Services in Johannesburg, South Africa</title>
  <meta name="description" content="Based in Johannesburg, South Africa, LunexWeb builds modern, responsive websites and strategic marketing campaigns that suit any business. We ensure every decision aligns with your brand and goals." />
  <meta name="keywords" content="about LunexWeb, Johannesburg web development, South Africa digital marketing, business websites, responsive design, marketing campaigns" />
</svelte:head>

<!-- Hero Section -->
<section class="pt-16 sm:pt-20 pb-16 sm:pb-20 bg-primary">
  <div class="container-custom px-4 text-center">
    <h1 class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-bold text-text mb-4 sm:mb-6 leading-tight">
      About LunexWeb
    </h1>
    <p class="text-lg sm:text-xl text-text/70 max-w-2xl sm:max-w-3xl mx-auto leading-relaxed">
      Professional web development and digital marketing services in Johannesburg, South Africa
    </p>
  </div>
</section>

<!-- About Content -->
<section bind:this={aboutContent} class="section-padding bg-primary">
  <div class="container-custom">
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 sm:gap-16 items-center">
      <div>
        <h2 class="text-2xl sm:text-3xl md:text-4xl font-bold text-text mb-4 sm:mb-6 leading-tight">
          Our Journey in Web Development & Digital Marketing
        </h2>
        <p class="text-base sm:text-lg text-text/70 mb-4 sm:mb-6 leading-relaxed">
          Based in Johannesburg, South Africa, LunexWeb builds modern, responsive websites and strategic marketing campaigns that suit any business. We believe every website is an investment, which is why we start by deeply understanding your business and target market before we quote.
        </p>
        <p class="text-base sm:text-lg text-text/70 mb-4 sm:mb-6 leading-relaxed">
          Our process is built on communication and transparency. We ensure every decision we make is aligned with your brand and your goals — helping you achieve measurable results and a strong return on investment.
        </p>
        <p class="text-base sm:text-lg text-text/70 leading-relaxed">
          Over the years, we've worked on projects ranging from simple landing pages to complex web applications, always staying current with the latest technologies including React, Svelte, HTML5, CSS3, JavaScript (ES6+), and Tailwind CSS. Each project has taught us something new about user experience, performance optimization, and the ever-evolving landscape of web technologies.
        </p>
      </div>
      
      <div class="relative">
        <div class="w-full h-64 sm:h-80 md:h-96 bg-gray-200 rounded-2xl overflow-hidden">
          <img 
            src="https://res.cloudinary.com/dnnwvmh3n/image/upload/v1754776156/courtney-cook-h7aVq-7FfPw-unsplash_bhftmk.jpg" 
            alt="Professional web development workspace" 
            class="w-full h-full object-cover rounded-2xl"
          />
        </div>
        <div class="absolute -bottom-2 sm:-bottom-4 -right-2 sm:-right-4 w-20 h-20 sm:w-32 sm:h-32 bg-black rounded-2xl opacity-10"></div>
      </div>
    </div>
  </div>
</section>

<!-- Skills Section -->
<section bind:this={skillsSection} class="section-padding bg-gray-50">
  <div class="container-custom">
    <div class="text-center mb-12 sm:mb-16">
      <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
        Our Core Skills
      </h2>
      <p class="text-lg sm:text-xl text-text/70 max-w-2xl mx-auto leading-relaxed">
        We combine technical expertise with creative problem-solving
      </p>
    </div>
    
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 sm:gap-8">
      <!-- Web Development -->
      <div class="skill-item bg-primary p-6 sm:p-8 rounded-2xl card-shadow">
        <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
          <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
          </svg>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">Web Development</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed">
          Modern web technologies including React, Svelte, HTML5, CSS3, JavaScript (ES6+), and Tailwind CSS. We create fast, responsive, and user-friendly websites.
        </p>
      </div>
      
      <!-- Digital Marketing -->
      <div class="skill-item bg-primary p-6 sm:p-8 rounded-2xl card-shadow">
        <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
          <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
          </svg>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">Digital Marketing</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed">
          Comprehensive digital marketing strategies including SEO, Google Ads, social media advertising, and content marketing to drive growth.
        </p>
      </div>
      
      <!-- User Experience -->
      <div class="skill-item bg-primary p-6 sm:p-8 rounded-2xl card-shadow">
        <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
          <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
          </svg>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">User Experience</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed">
          User-centered design principles ensuring intuitive navigation, accessibility, and engaging user experiences across all devices.
        </p>
      </div>
      
      <!-- Performance Optimization -->
      <div class="skill-item bg-primary p-6 sm:p-8 rounded-2xl card-shadow">
        <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
          <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
          </svg>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">Performance Optimization</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed">
          Fast-loading websites with optimized images, efficient code, and modern performance techniques for better user engagement.
        </p>
      </div>
      
      <!-- SEO & Analytics -->
      <div class="skill-item bg-primary p-6 sm:p-8 rounded-2xl card-shadow">
        <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
          <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
          </svg>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">SEO & Analytics</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed">
          Search engine optimization and data-driven insights to improve visibility and track performance for continuous improvement.
        </p>
      </div>
      
      <!-- Mobile-First Design -->
      <div class="skill-item bg-primary p-6 sm:p-8 rounded-2xl card-shadow">
        <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
          <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z" />
          </svg>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">Mobile-First Design</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed">
          Responsive design that works perfectly on all devices, from mobile phones to desktop computers.
        </p>
      </div>
    </div>
  </div>
</section>

<!-- Experience Section -->
<section bind:this={experienceSection} class="section-padding bg-primary">
  <div class="container-custom">
    <div class="text-center mb-12 sm:mb-16">
      <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
        Our Experience
      </h2>
      <p class="text-lg sm:text-xl text-text/70 max-w-2xl mx-auto leading-relaxed">
        Years of experience delivering successful projects across various industries
      </p>
    </div>
    
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8 sm:gap-12">
      <!-- Project Count -->
      <div class="experience-item text-center p-6 sm:p-8 bg-gray-50 rounded-2xl">
        <div class="text-4xl sm:text-5xl md:text-6xl font-bold text-text mb-4">50+</div>
        <h3 class="text-xl sm:text-2xl font-bold text-text mb-3">Projects Completed</h3>
        <p class="text-sm sm:text-base text-text/70">
          From small business websites to complex web applications, we've successfully delivered projects that exceed expectations.
        </p>
      </div>
      
      <!-- Client Satisfaction -->
      <div class="experience-item text-center p-6 sm:p-8 bg-gray-50 rounded-2xl">
        <div class="text-4xl sm:text-5xl md:text-6xl font-bold text-text mb-4">98%</div>
        <h3 class="text-xl sm:text-2xl font-bold text-text mb-3">Client Satisfaction</h3>
        <p class="text-sm sm:text-base text-text/70">
          Our commitment to quality and communication has resulted in high client satisfaction rates and long-term partnerships.
        </p>
      </div>
      
      <!-- Years of Experience -->
      <div class="experience-item text-center p-6 sm:p-8 bg-gray-50 rounded-2xl">
        <div class="text-4xl sm:text-5xl md:text-6xl font-bold text-text mb-4">5+</div>
        <h3 class="text-xl sm:text-2xl font-bold text-text mb-3">Years of Experience</h3>
        <p class="text-sm sm:text-base text-text/70">
          Years of experience in web development and digital marketing, staying current with the latest technologies and trends.
        </p>
      </div>
      
      <!-- Technologies Mastered -->
      <div class="experience-item text-center p-6 sm:p-8 bg-gray-50 rounded-2xl">
        <div class="text-4xl sm:text-5xl md:text-6xl font-bold text-text mb-4">15+</div>
        <h3 class="text-xl sm:text-2xl font-bold text-text mb-3">Technologies Mastered</h3>
        <p class="text-sm sm:text-base text-text/70">
          From frontend frameworks to backend technologies, we've mastered a wide range of tools and platforms.
        </p>
      </div>
    </div>
  </div>
</section>

<!-- Values Section -->
<section class="section-padding bg-gray-50">
  <div class="container-custom">
    <div class="text-center mb-12 sm:mb-16">
      <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
        Our Values
      </h2>
      <p class="text-lg sm:text-xl text-text/70 max-w-2xl mx-auto leading-relaxed">
        The principles that guide everything we do
      </p>
    </div>
    
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8 sm:gap-12">
      <!-- Quality -->
      <div class="text-center">
        <div class="w-16 h-16 sm:w-20 sm:h-20 bg-text rounded-full mx-auto mb-4 sm:mb-6 flex items-center justify-center">
          <svg class="w-8 h-8 sm:w-10 sm:h-10 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3">Quality</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed">
          We never compromise on quality. Every project is built with attention to detail and best practices.
        </p>
      </div>
      
      <!-- Communication -->
      <div class="text-center">
        <div class="w-16 h-16 sm:w-20 sm:h-20 bg-text rounded-full mx-auto mb-4 sm:mb-6 flex items-center justify-center">
          <svg class="w-8 h-8 sm:w-10 sm:h-10 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
          </svg>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3">Communication</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed">
          Clear, transparent communication throughout the project ensures you're always informed and involved.
        </p>
      </div>
      
      <!-- Results -->
      <div class="text-center">
        <div class="w-16 h-16 sm:w-20 sm:h-20 bg-text rounded-full mx-auto mb-4 sm:mb-6 flex items-center justify-center">
          <svg class="w-8 h-8 sm:w-10 sm:h-10 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6" />
          </svg>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3">Results</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed">
          We focus on delivering measurable results that help your business grow and succeed online.
        </p>
      </div>
    </div>
  </div>
</section>

<!-- CTA Section -->
<section class="section-padding bg-primary">
  <div class="container-custom text-center">
    <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
      Ready to Work Together?
    </h2>
    <p class="text-lg sm:text-xl text-text/70 mb-8 sm:mb-10 max-w-2xl mx-auto leading-relaxed">
      Let's discuss your project and create something amazing that drives real business results.
    </p>
    <div class="flex flex-col sm:flex-row items-center justify-center gap-4 sm:gap-6">
      <a href="/contact" class="btn-primary text-base sm:text-lg px-6 sm:px-8 py-3 sm:py-4 w-full sm:w-auto">
        Get in Touch
      </a>
      <a href="/websites" class="btn-secondary text-base sm:text-lg px-6 sm:px-8 py-3 sm:py-4 w-full sm:w-auto">
        View Our Work
      </a>
    </div>
  </div>
</section> 