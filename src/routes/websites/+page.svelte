<script>
  import { onMount } from 'svelte';
  import { page } from '$app/stores';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  import OptimizedVideo from '$lib/OptimizedVideo.svelte';
  
  gsap.registerPlugin(ScrollTrigger);
  
  let websitesGrid;
  let filterButtons;
  
  // Websites data
  const projects = [
    {
      id: 1,
      title: "E-Commerce Platform",
      category: "web-app",
      description: "Modern online store with advanced features, payment integration, and mobile-first design.",
      technologies: ["React", "Node.js", "Stripe", "MongoDB"],
      image: "/api/placeholder/600/400",
      link: "#"
    },
    {
      id: 2,
      title: "Corporate Website",
      category: "website",
      description: "Professional business website with modern design and smooth animations.",
      technologies: ["Svelte", "GSAP", "TailwindCSS"],
      image: "/api/placeholder/600/400",
      link: "#"
    },
    {
      id: 3,
      title: "Portfolio Website",
      category: "website",
      description: "Creative portfolio showcasing artistic work with interactive elements.",
      technologies: ["Vue.js", "Three.js", "CSS3"],
      image: "/api/placeholder/600/400",
      link: "#"
    },
    {
      id: 4,
      title: "Dashboard Application",
      category: "web-app",
      description: "Real-time dashboard with data visualization and interactive charts.",
      technologies: ["Vue.js", "D3.js", "WebSocket", "Express"],
      image: "/api/placeholder/600/400",
      link: "#"
    },
    {
      id: 5,
      title: "Mobile App Landing",
      category: "landing",
      description: "High-converting landing page for mobile application with A/B testing.",
      technologies: ["React", "Framer Motion", "Analytics"],
      image: "/api/placeholder/600/400",
      link: "#"
    },
    {
      id: 6,
      title: "Restaurant Website",
      category: "website",
      description: "Elegant restaurant website with online ordering and reservation system.",
      technologies: ["Svelte", "Stripe", "PostgreSQL"],
      image: "/api/placeholder/600/400",
      link: "#"
    },
    {
      id: 7,
      title: "SEO Campaign",
      category: "marketing",
      description: "Comprehensive SEO strategy that increased organic traffic by 300% in 6 months.",
      technologies: ["Keyword Research", "On-Page SEO", "Link Building", "Analytics"],
      image: "/api/placeholder/600/400",
      link: "#"
    },
    {
      id: 8,
      title: "Google Ads Campaign",
      category: "marketing",
      description: "Targeted PPC campaign with 25% increase in conversion rate and 40% reduction in cost per acquisition.",
      technologies: ["Google Ads", "Conversion Tracking", "A/B Testing", "Remarketing"],
      image: "/api/placeholder/600/400",
      link: "#"
    },
    {
      id: 9,
      title: "Social Media Strategy",
      category: "marketing",
      description: "Multi-platform social media campaign that grew audience by 500% and increased engagement by 200%.",
      technologies: ["Facebook Ads", "Instagram", "LinkedIn", "Content Creation"],
      image: "/api/placeholder/600/400",
      link: "#"
    }
  ];
  
  let activeFilter = 'all';
  let filteredProjects = projects;
  
  function filterProjects(category) {
    activeFilter = category;
    if (category === 'all') {
      filteredProjects = projects;
    } else {
      filteredProjects = projects.filter(project => project.category === category);
    }
    
    // Animate filtered projects
    gsap.fromTo(filteredProjects, 
      { opacity: 0, y: 20 },
      { 
        opacity: 1, 
        y: 0, 
        duration: 0.6, 
        ease: "power3.out",
        stagger: 0.1
      }
    );
  }
  
  onMount(() => {
    // Websites grid animation
    gsap.fromTo(websitesGrid.querySelectorAll('.website-item'), 
      { opacity: 0, y: 30 },
      { 
        opacity: 1, 
        y: 0, 
        duration: 0.8, 
        ease: "power3.out",
        stagger: 0.15,
        scrollTrigger: {
          trigger: websitesGrid,
          start: "top 80%",
          end: "bottom 20%",
          toggleActions: "play none none reverse"
        }
      }
    );
    
    // Filter buttons animation
    gsap.fromTo(filterButtons.querySelectorAll('button'), 
      { opacity: 0, y: 20 },
      { 
        opacity: 1, 
        y: 0, 
        duration: 0.6, 
        ease: "power3.out",
        stagger: 0.1,
        delay: 0.3
      }
    );
  });
</script>

<svelte:head>
  <title>Websites & Marketing Services - LunexWeb | Modern Web Design & Digital Marketing in Johannesburg</title>
  <meta name="description" content="LunexWeb creates websites that combine style with performance. Our designs are mobile-friendly, fast-loading, and tailored to your brand identity. From SEO to social media marketing, we help you get found online." />
  <meta name="keywords" content="website design Johannesburg, digital marketing services, modern web design, mobile-friendly websites, SEO services, social media marketing, business websites" />
</svelte:head>

<!-- Hero Section -->
<section class="pt-16 sm:pt-20 pb-16 sm:pb-20 bg-primary relative overflow-hidden">
  <!-- Background Video -->
  <div class="absolute inset-0 z-0 h-full w-full">
    <OptimizedVideo
      src="https://res.cloudinary.com/dnnwvmh3n/video/upload/v1755168588/lambo_1_bjuyqi.mp4"
      autoplay={true}
      muted={true}
      loop={true}
      playsinline={true}
      preload="auto"
      class_name="w-full h-full absolute inset-0"
      objectFit="cover"
      objectPosition="center"
      alt="Professional web development and digital marketing services background"
    />
  </div>
  
  <div class="container-custom px-4 text-center relative z-10">
    <h1 class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-bold text-text mb-4 sm:mb-6 leading-tight">
      Websites & Marketing Services
    </h1>
    <p class="text-lg sm:text-xl text-text/70 max-w-2xl sm:max-w-3xl mx-auto leading-relaxed">
      Professional web development services showcasing modern websites, web applications, and digital solutions built with cutting-edge technologies
    </p>
  </div>
</section>

<!-- What We Do Section with Video -->
<section class="section-padding bg-primary">
  <div class="container-custom">
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 sm:gap-16 items-center">
      <!-- Content -->
      <div>
        <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-6 sm:mb-8 leading-tight">
          Professional Web Development Services
        </h2>
        <p class="text-base sm:text-lg text-text/70 mb-6 sm:mb-8 leading-relaxed">
          We specialize in creating high-performance, responsive websites and web applications that deliver exceptional user experiences. Our expertise spans from frontend development using modern frameworks like React and Svelte to comprehensive digital marketing solutions that drive business growth and improve search engine rankings.
        </p>
        
        <!-- Services -->
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 sm:gap-6">
          <div class="text-center p-4 bg-secondary/20 rounded-lg subtle-border">
            <div class="w-10 h-10 sm:w-12 sm:h-12 bg-secondary rounded-lg mx-auto mb-2 sm:mb-3 flex items-center justify-center">
              <svg class="w-5 h-5 sm:w-6 sm:h-6 text-text" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
              </svg>
            </div>
            <h4 class="font-semibold text-text text-sm sm:text-base">Web Development</h4>
            <p class="text-xs sm:text-sm text-text/70 mt-2">React, Svelte, HTML, CSS, JavaScript, Tailwind CSS</p>
          </div>
          
          <div class="text-center p-4 bg-secondary/20 rounded-lg subtle-border">
            <div class="w-10 h-10 sm:w-12 sm:h-12 bg-secondary rounded-lg mx-auto mb-2 sm:mb-3 flex items-center justify-center">
              <svg class="w-5 h-5 sm:w-6 sm:h-6 text-text" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
              </svg>
            </div>
            <h4 class="font-semibold text-text text-sm sm:text-base">Digital Marketing</h4>
            <p class="text-xs sm:text-sm text-text/70 mt-2">SEO, Google Ads, Social Media Ads, Social Media Management</p>
          </div>
        </div>
      </div>
      
      <!-- Laptop Mockup with Video -->
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
</section>

<!-- Portfolio Section -->
<section class="section-padding bg-gray-50">
  <div class="container-custom">
    <div class="text-center mb-12 sm:mb-16">
      <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
        Our Work
      </h2>
      <p class="text-lg sm:text-xl text-text/70 max-w-2xl mx-auto leading-relaxed">
        Check out our latest projects and see how we bring ideas to life
      </p>
    </div>
    
    <!-- Filter Buttons -->
    <div bind:this={filterButtons} class="flex flex-wrap justify-center gap-3 sm:gap-4 mb-8 sm:mb-12">
      <button 
        class="filter-btn px-4 sm:px-6 py-2 sm:py-3 rounded-lg font-medium text-sm sm:text-base {activeFilter === 'all' ? 'bg-text text-primary' : 'bg-primary text-text hover:bg-text hover:text-primary'}"
        on:click={() => filterProjects('all')}
      >
        All Projects
      </button>
      <button 
        class="filter-btn px-4 sm:px-6 py-2 sm:py-3 rounded-lg font-medium text-sm sm:text-base {activeFilter === 'website' ? 'bg-text text-primary' : 'bg-primary text-text hover:bg-text hover:text-primary'}"
        on:click={() => filterProjects('website')}
      >
        Websites
      </button>
      <button 
        class="filter-btn px-4 sm:px-6 py-2 sm:py-3 rounded-lg font-medium text-sm sm:text-base {activeFilter === 'web-app' ? 'bg-text text-primary' : 'bg-primary text-text hover:bg-text hover:text-primary'}"
        on:click={() => filterProjects('web-app')}
      >
        Web Applications
      </button>
      <button 
        class="filter-btn px-4 sm:px-6 py-2 sm:py-3 rounded-lg font-medium text-sm sm:text-base {activeFilter === 'landing' ? 'bg-text text-primary' : 'bg-primary text-text hover:bg-text hover:text-primary'}"
        on:click={() => filterProjects('landing')}
      >
        Landing Pages
      </button>
      <button 
        class="filter-btn px-4 sm:px-6 py-2 sm:py-3 rounded-lg font-medium text-sm sm:text-base {activeFilter === 'marketing' ? 'bg-text text-primary' : 'bg-primary text-text hover:bg-text hover:text-primary'}"
        on:click={() => filterProjects('marketing')}
      >
        Digital Marketing
      </button>
    </div>
    
    <!-- Projects Grid -->
    <div bind:this={websitesGrid} class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 sm:gap-8">
      {#each filteredProjects as project}
        <div class="website-item bg-primary rounded-2xl overflow-hidden card-shadow hover:-translate-y-2 transition-all duration-300">
          <!-- Project Content -->
          <div class="p-4 sm:p-6">
            <h3 class="text-lg sm:text-xl font-bold text-text mb-2 sm:mb-3 leading-tight">
              {project.title}
            </h3>
            <p class="text-sm sm:text-base text-text/70 mb-4 leading-relaxed">
              {project.description}
            </p>
            
            <!-- Technologies -->
            <div class="flex flex-wrap gap-2">
              {#each project.technologies as tech}
                <span class="px-2 sm:px-3 py-1 bg-gray-100 text-text text-xs sm:text-sm rounded-full font-medium">
                  {tech}
                </span>
              {/each}
            </div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- Services Overview -->
<section class="section-padding bg-primary">
  <div class="container-custom">
    <div class="text-center mb-12 sm:mb-16">
      <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
        Our Services
      </h2>
      <p class="text-lg sm:text-xl text-text/70 max-w-2xl mx-auto leading-relaxed">
        Comprehensive web development and digital marketing solutions
      </p>
    </div>
    
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 sm:gap-8">
      <!-- Web Development -->
      <div class="bg-gray-50 p-6 sm:p-8 rounded-2xl card-shadow hover:-translate-y-2 transition-all duration-300">
        <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
          <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
          </svg>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">Web Development</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed mb-4 sm:mb-6">
          Custom websites and web applications built with modern technologies. We focus on performance, user experience, and scalability.
        </p>
        <ul class="text-sm sm:text-base text-text/70 space-y-2">
          <li>• Responsive design for all devices</li>
          <li>• Modern frameworks (React, Svelte, Vue)</li>
          <li>• Performance optimization</li>
          <li>• SEO-friendly code structure</li>
        </ul>
      </div>
      
      <!-- Digital Marketing -->
      <div class="bg-gray-50 p-6 sm:p-8 rounded-2xl card-shadow hover:-translate-y-2 transition-all duration-300">
        <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
          <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
          </svg>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">Digital Marketing</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed mb-4 sm:mb-6">
          Strategic digital marketing campaigns that drive traffic, increase conversions, and grow your business online.
        </p>
        <ul class="text-sm sm:text-base text-text/70 space-y-2">
          <li>• Search Engine Optimization (SEO)</li>
          <li>• Google Ads & PPC campaigns</li>
          <li>• Social media advertising</li>
          <li>• Content marketing strategies</li>
        </ul>
      </div>
      
      <!-- E-commerce Solutions -->
      <div class="bg-gray-50 p-6 sm:p-8 rounded-2xl card-shadow hover:-translate-y-2 transition-all duration-300">
        <div class="w-12 h-12 sm:w-16 sm:h-16 bg-text rounded-xl mb-4 sm:mb-6 flex items-center justify-center">
          <svg class="w-6 h-6 sm:w-8 sm:h-8 text-primary" fill="none" stroke="black" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z" />
          </svg>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3 sm:mb-4">E-commerce Solutions</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed mb-4 sm:mb-6">
          Complete online store solutions with secure payment processing, inventory management, and customer experience optimization.
        </p>
        <ul class="text-sm sm:text-base text-text/70 space-y-2">
          <li>• Secure payment gateways</li>
          <li>• Inventory management systems</li>
          <li>• Customer account portals</li>
          <li>• Analytics and reporting</li>
        </ul>
      </div>
    </div>
  </div>
</section>

<!-- Process Section -->
<section class="section-padding bg-gray-50">
  <div class="container-custom">
    <div class="text-center mb-12 sm:mb-16">
      <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
        Our Process
      </h2>
      <p class="text-lg sm:text-xl text-text/70 max-w-2xl mx-auto leading-relaxed">
        How we work to deliver exceptional results
      </p>
    </div>
    
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6 sm:gap-8">
      <!-- Step 1 -->
      <div class="text-center">
        <div class="w-16 h-16 sm:w-20 sm:h-20 bg-text rounded-full mx-auto mb-4 sm:mb-6 flex items-center justify-center">
          <span class="text-primary font-bold text-xl sm:text-2xl">1</span>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3">Discovery</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed">
          We start by understanding your business goals, target audience, and project requirements.
        </p>
      </div>
      
      <!-- Step 2 -->
      <div class="text-center">
        <div class="w-16 h-16 sm:w-20 sm:h-20 bg-text rounded-full mx-auto mb-4 sm:mb-6 flex items-center justify-center">
          <span class="text-primary font-bold text-xl sm:text-2xl">2</span>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3">Planning</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed">
          We create detailed project plans, wireframes, and design concepts for your approval.
        </p>
      </div>
      
      <!-- Step 3 -->
      <div class="text-center">
        <div class="w-16 h-16 sm:w-20 sm:h-20 bg-text rounded-full mx-auto mb-4 sm:mb-6 flex items-center justify-center">
          <span class="text-primary font-bold text-xl sm:text-2xl">3</span>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3">Development</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed">
          Our team builds your project using modern technologies and best practices.
        </p>
      </div>
      
      <!-- Step 4 -->
      <div class="text-center">
        <div class="w-16 h-16 sm:w-20 sm:h-20 bg-text rounded-full mx-auto mb-4 sm:mb-6 flex items-center justify-center">
          <span class="text-primary font-bold text-xl sm:text-2xl">4</span>
        </div>
        <h3 class="text-lg sm:text-xl font-bold text-text mb-3">Launch</h3>
        <p class="text-sm sm:text-base text-text/70 leading-relaxed">
          We deploy your project and provide ongoing support to ensure success.
        </p>
      </div>
    </div>
  </div>
</section>

<!-- CTA Section -->
<section class="section-padding bg-primary">
  <div class="container-custom text-center">
    <h2 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold text-text mb-4 sm:mb-6 leading-tight">
      Ready to Start Your Project?
    </h2>
    <p class="text-lg sm:text-xl text-text/70 mb-8 sm:mb-10 max-w-2xl mx-auto leading-relaxed">
      Let's discuss your ideas and create something amazing that drives real business results.
    </p>
    <div class="flex flex-col sm:flex-row items-center justify-center gap-4 sm:gap-6">
      <a href="/contact" class="btn-primary text-base sm:text-lg px-6 sm:px-8 py-3 sm:py-4 w-full sm:w-auto">
        Get Started
      </a>
      <a href="/about" class="btn-secondary text-base sm:text-lg px-6 sm:px-8 py-3 sm:py-4 w-full sm:w-auto">
        Learn More
      </a>
    </div>
  </div>
</section> 