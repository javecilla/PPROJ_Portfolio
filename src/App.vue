<script setup>
import { onMounted, ref, defineAsyncComponent } from "vue";
import AOS from "aos";
import GLightbox from 'glightbox';
import Swiper from 'swiper';

import PageLoader from '@/components/PageLoader.vue';
import BackToTop from '@/components/BackToTop.vue';

const AppHeader = defineAsyncComponent(() => import('@/components/AppHeader.vue'));
const AppFooter = defineAsyncComponent(() => import('@/components/AppFooter.vue'));

const swiperConfig = ref({
  loop: true,
  speed: 600,
  autoplay: {
    delay: 5000
  },
  slidesPerView: "auto",
  pagination: {
    el: ".swiper-pagination",
    type: "bullets",
    clickable: true
  },
  breakpoints: {
    320: {
      slidesPerView: 1,
      spaceBetween: 40
    },
    1200: {
      slidesPerView: 3,
      spaceBetween: 1
    }
  }
});


onMounted(() => {
  AOS.init();
  GLightbox({ selector: '.glightbox' });

  /**
   * Initializes the AOS (Animate On Scroll) library with custom settings
   */
  function aosInit() {
    AOS.init({
      duration: 600,
      easing: 'ease-in-out',
      once: true,
      mirror: false
    });
  }

  /**
   * Initializes Swiper instances for all elements with the 'init-swiper' class
   * Uses the swiperConfig for testimonials
   */
  function initSwiper() {
    document.querySelectorAll(".init-swiper").forEach(function(swiperElement) {
      new Swiper(swiperElement, swiperConfig.value);
    });
  }

  window.addEventListener('load', aosInit);

  /**
   * Frequently Asked Questions Toggle
   */
  document.querySelectorAll('.faq-item h3, .faq-item .faq-toggle').forEach((faqItem) => {
    faqItem.addEventListener('click', () => {
      faqItem.parentNode.classList.toggle('faq-active');
    });
  });

 /**
   * Correct scrolling position for hash links
   * Adjusts scroll position when page loads with a hash in the URL
   */
  window.addEventListener('load', () => {
    if (window.location.hash) {
      if (document.querySelector(window.location.hash)) {
        setTimeout(() => {
          let section = document.querySelector(window.location.hash);
          let scrollMarginTop = getComputedStyle(section).scrollMarginTop;
          window.scrollTo({
            top: section.offsetTop - parseInt(scrollMarginTop),
            behavior: 'smooth'
          });
        }, 100);
      }
    }
  });

  // Initialize functions
  initSwiper();
  aosInit();
});
</script>

<template>
  <Suspense>
    <template #default>
      <div>
        <AppHeader /> 

        <main class="main">
          <!-- Hero Section -->
          <section id="hero" class="hero section">
            <div class="hero-bg">
              <img src="@/assets/img/hero-bg-light.webp" alt="">
            </div>
            <div class="container text-center">
              <div class="d-flex flex-column justify-content-center align-items-center">
                <h1 data-aos="fade-up">Hello, I'm <span>Jerome Avecilla</span></h1>
                <label data-aos="fade-up" data-aos-delay="100" class="profession">Aspiring Web Developer</label>
                <p data-aos="fade-up" data-aos-delay="200">Dedicated BSIT student passionate about creating innovative web solutions.<br></p>
                <div class="d-flex" data-aos="fade-up" data-aos-delay="300">
                  <a href="#about" class="btn-get-in-touch"> Get in Touch</a>
                  <a href="https://www.youtube.com/watch?v=Y7f98aduVJ8" class="glightbox btn-watch-video d-flex align-items-center"><i class="bi bi-arrow-down-circle"></i><span>Download CV</span></a>
                </div>
                <img src="@/assets/img/hero-services-img.webp" class="img-fluid hero-img" alt="" data-aos="zoom-out" data-aos-delay="300">
              </div>
            </div>
          </section><!-- /Hero Section -->

          <!-- Featured Services Section -->
          <section id="featured-services" class="featured-services section light-background">
            <div class="container">

              <div class="row gy-4">

                <div class="col-xl-4 col-lg-6" data-aos="fade-up" data-aos-delay="100">
                  <div class="service-item d-flex">
                    <div class="icon flex-shrink-0"><i class="bi bi-code-slash"></i></div>
                    <div>
                      <h4 class="title"><a href="#" class="stretched-link">Front End Development</a></h4>
                      <p class="description">Crafting responsive and intuitive user interfaces using Vue.js and modern web technologies to deliver seamless user experiences.</p>
                    </div>
                  </div>
                </div>
                <!-- End Service Item -->

                <div class="col-xl-4 col-lg-6" data-aos="fade-up" data-aos-delay="200">
                  <div class="service-item d-flex">
                    <div class="icon flex-shrink-0"><i class="bi bi-braces"></i></div>
                    <div>
                      <h4 class="title"><a href="#" class="stretched-link">Back End Development</a></h4>
                      <p class="description">Building robust and scalable server-side applications with Laravel, ensuring efficient data management and API integrations.</p>
                    </div>
                  </div>
                </div><!-- End Service Item -->

                <div class="col-xl-4 col-lg-6" data-aos="fade-up" data-aos-delay="300">
                  <div class="service-item d-flex">
                    <div class="icon flex-shrink-0"><i class="bi bi-globe"></i></div>
                    <div>
                      <h4 class="title"><a href="#" class="stretched-link">DevOps & Deployment</a></h4>
                      <p class="description">Implementing best practices in continuous integration and deployment (CI/CD) to ensure smooth, efficient, and reliable web application delivery.</p>
                    </div>
                  </div>
                </div><!-- End Service Item -->

              </div>

            </div>
          </section><!-- /Featured Services Section -->

          <!-- About Section -->
          <section id="about" class="about section">
            <div class="container">

              <div class="row gy-4">

                <div class="col-lg-6 content" data-aos="fade-up" data-aos-delay="100">
                  <p class="who-we-are">About me</p>
                  <h3>Aspiring Web Developer</h3>
                  <p >
                    As a dedicated second-year BSIT student, I am on a mission to become a proficient and innovative web developer, constantly pushing the boundaries of what's possible in the digital realm.
                  </p>
                  <p>
                    Since embarking on my web development journey in 2021, I have cultivated a deep passion for coding and problem-solving. My expertise spans HTML, CSS, and JavaScript, forming a solid foundation for creating responsive and user-centric web applications. I am particularly enthusiastic about modern frameworks like Vue.js and backend technologies such as Laravel, which I leverage to build robust, scalable solutions.
                  </p>
                  <ul class="fst-italic">
                    <li><i class="bi bi-check-circle"></i> <span>Committed to continuous learning and staying abreast of emerging technologies</span></li>
                    <li><i class="bi bi-check-circle"></i> <span>Experienced in developing responsive, user-friendly interfaces</span></li>
                    <li><i class="bi bi-check-circle"></i> <span>Passionate about creating efficient, scalable web solutions</span></li>
                  </ul>
                </div>

                <div class="col-lg-6 about-images" data-aos="fade-up" data-aos-delay="200">
                  <div class="row gy-4">
                    <div class="col-lg-6">
                      <img src="@/assets/img/about-company-1.jpg" class="img-fluid" alt="">
                    </div>
                    <div class="col-lg-6">
                      <div class="row gy-4">
                        <div class="col-lg-12">
                          <img src="@/assets/img/about-company-2.jpg" class="img-fluid" alt="">
                        </div>
                        <div class="col-lg-12">
                          <img src="@/assets/img/about-company-3.jpg" class="img-fluid" alt="">
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </section><!-- /About Section -->

         <!-- Skills Section -->
          <section id="skills" class="skills section">
            <div class="container" data-aos="fade-up">
              <!-- Section Title -->
              <div class="container section-title" data-aos="fade-up">
                <h2>Languages and Tools</h2>
                <p>I'm thrilled to share my web development tech stack and skills. With ongoing learning and a passion for innovation, I continuously expand my knowledge to improve my skills and stay ahead of industry trends.</p>
              </div><!-- End Section Title -->
  
              <div class="row">
                <!-- Front-End Skills -->
                <div class="col-lg-3 col-md-6">
                  <div class="skill-category">
                    <h4>Front-End</h4>
                    <div class="skill-icons">
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg" title="HTML5" alt="HTML5" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg" title="CSS3" alt="CSS3" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg" title="JavaScript" alt="JavaScript" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg" title="Vue.js" alt="Vue.js" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/bootstrap/bootstrap-original.svg" title="Bootstrap" alt="Bootstrap" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/jquery/jquery-original.svg" title="jQuery" alt="jQuery" loading="lazy"/>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Back-End Skills -->
                <div class="col-lg-3 col-md-6">
                  <div class="skill-category">
                    <h4>Back-End</h4>
                    <div class="skill-icons">
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/php/php-original.svg" title="PHP" alt="PHP" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/laravel/laravel-original.svg" title="Laravel" alt="Laravel" loading="lazy"/>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Database Skills -->
                <div class="col-lg-3 col-md-6">
                  <div class="skill-category">
                    <h4>Databases</h4>
                    <div class="skill-icons">
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mysql/mysql-original-wordmark.svg" title="MySQL" alt="MySQL" loading="lazy"/>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- DevOps Skills -->
                <div class="col-lg-3 col-md-6">
                  <div class="skill-category">
                    <h4>DevOps & CI/CD</h4>
                    <div class="skill-icons">
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg" title="Git" alt="Git" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/gitlab/gitlab-original.svg" title="GitLab" alt="GitLab" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/githubactions/githubactions-original.svg" title="GitHub Actions" alt="GitHub Actions" loading="lazy"/>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Development Tools -->
                <div class="col-lg-3 col-md-6">
                  <div class="skill-category">
                    <h4>Development Tools</h4>
                    <div class="skill-icons">
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vscode/vscode-original.svg" title="VS Code" alt="VS Code" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://upload.wikimedia.org/wikipedia/en/d/d2/Sublime_Text_3_logo.png" title="Sublime Text" alt="Sublime Text" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/d/dc/XAMPP_Logo.png" title="XAMPP Control Panel" alt="XAMPP Control Panel" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://img.utdstc.com/icon/f6f/11c/f6f11c75fda63dd454fa5db9610a77cfd6752be4db11010f2e4252551a4abccd:200" title="MySQL Workbench" alt="MySQL Workbench" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/postman/postman-original.svg" title="Postman" alt="Postman" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://testdev.tools/images/resources/httpie.png" title="Httpie" alt="Httpie" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/figma/figma-original.svg" title="Figma" alt="Figma" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSOYxPmG8LC5HCIw74mb5EMVSOxFjpQQ3aGjg&s" title="Github Desktop" alt="Github Desktop" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.worldvectorlogo.com/logos/git-bash.svg" title="Gitbash" alt="Gitbash" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/bash/bash-original.svg" title="CMD" alt="CMD" loading="lazy"/>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Web Hosting (Experience) -->
                <div class="col-lg-3 col-md-6">
                  <div class="skill-category">
                    <h4>Web Hosting (Experience)</h4>
                    <div class="skill-icons">
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg" title="Github Pages" alt="Github Pages" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://seeklogo.com/images/V/vercel-logo-F748E39008-seeklogo.com.png" title="Vercel" alt="Vercel" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRXeNlCtJpIjX0MieB0Jdtx5xI2iKL-AUJCYw&s" title="CPanel" alt="CPanel" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRaB-WOkNWv3EnGpOd8mR8-Kj3qFzSxTaJvAg&s" title="Hostgator" alt="Hostgator" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRs5tIW0piUCQGICpqFHolVv8QSR1ryqZ_kww&s" title="Go Daddy" alt="Go Daddy" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://www.elegantthemes.com/blog/wp-content/uploads/2024/05/Hostinger-Logo.png" title="Hostinger" alt="Hostinger" loading="lazy"/>
                      </div>
                   </div>
                  </div>
                </div>

                <!-- Others -->
                <div class="col-lg-3 col-md-6">
                  <div class="skill-category">
                    <h4>Others</h4>
                    <div class="skill-icons">
                      <div class="skill-icon">
                        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTY3X0aV2kvIeIx6PzwD6umKbuOES5JfOwRgA&s" title="CDN JS" alt="CDN JS" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.worldvectorlogo.com/logos/composer.svg" title="Composer" alt="Composer" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT9SjIbMYa0n2RMI8sDmIHkExRRpezpAP_-7A&" title="Symfony" alt="Symfony" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg" title="Node JS Runtime" alt="Node JS Runtime" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/npm/npm-original-wordmark.svg" title="NPM" alt="NPM" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f1/Vitejs-logo.svg/1039px-Vitejs-logo.svg.png" title="Vite" alt="Vite" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://static.canva.com/static/images/favicon-1.ico" title="Canva" alt="Canva" loading="lazy"/>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Currently Learning -->
                <div class="col-lg-3 col-md-6">
                  <div class="skill-category">
                    <h4>Currently Learning</h4>
                    <div class="skill-icons">
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg" title="TypeScript" alt="TypeScript" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/tailwindcss/tailwindcss-original.svg" title="Tailwind CS" alt="Tailwind CSS" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" title="Docker" alt="Docker" loading="lazy"/>
                      </div>
                      <div class="skill-icon">
                        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/microsoftsqlserver/microsoftsqlserver-original-wordmark.svg" title="MS SQL Server" alt="MS SQL Server" loading="lazy"/>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </section><!-- /Skills Section -->
          
          <!-- Features Section -->
          <section id="features" class="features section">
            <!-- Section Title -->
            <div class="container section-title" data-aos="fade-up">
              <h2>Features</h2>
              <p>Necessitatibus eius consequatur ex aliquid fuga eum quidem sint consectetur velit</p>
            </div><!-- End Section Title -->

            <div class="container">
              <div class="row justify-content-between">

                <div class="col-lg-5 d-flex align-items-center">

                  <ul class="nav nav-tabs" data-aos="fade-up" data-aos-delay="100">
                    <li class="nav-item">
                      <a class="nav-link active show" data-bs-toggle="tab" data-bs-target="#features-tab-1">
                        <i class="bi bi-binoculars"></i>
                        <div>
                          <h4 class="d-none d-lg-block">Modi sit est dela pireda nest</h4>
                          <p>
                            Ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate
                            velit esse cillum dolore eu fugiat nulla pariatur
                          </p>
                        </div>
                      </a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link" data-bs-toggle="tab" data-bs-target="#features-tab-2">
                        <i class="bi bi-box-seam"></i>
                        <div>
                          <h4 class="d-none d-lg-block">Unde praesenti mara setra le</h4>
                          <p>
                            Recusandae atque nihil. Delectus vitae non similique magnam molestiae sapiente similique
                            tenetur aut voluptates sed voluptas ipsum voluptas
                          </p>
                        </div>
                      </a>
                    </li>
                    <li class="nav-item">
                      <a class="nav-link" data-bs-toggle="tab" data-bs-target="#features-tab-3">
                        <i class="bi bi-brightness-high"></i>
                        <div>
                          <h4 class="d-none d-lg-block">Pariatur explica nitro dela</h4>
                          <p>
                            Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum
                            Debitis nulla est maxime voluptas dolor aut
                          </p>
                        </div>
                      </a>
                    </li>
                  </ul><!-- End Tab Nav -->

                </div>

                <div class="col-lg-6">

                  <div class="tab-content" data-aos="fade-up" data-aos-delay="200">

                    <div class="tab-pane fade active show" id="features-tab-1">
                      <img src="@/assets/img/tabs-1.jpg" alt="" class="img-fluid">
                    </div><!-- End Tab Content Item -->

                    <div class="tab-pane fade" id="features-tab-2">
                      <img src="@/assets/img/tabs-2.jpg" alt="" class="img-fluid">
                    </div><!-- End Tab Content Item -->

                    <div class="tab-pane fade" id="features-tab-3">
                      <img src="@/assets/img/tabs-3.jpg" alt="" class="img-fluid">
                    </div><!-- End Tab Content Item -->
                  </div>

                </div>

              </div>

            </div>
          </section><!-- /Features Section -->

          <!-- Features Details Section -->
          <section id="features-details" class="features-details section">
            <div class="container">

            <div class="row gy-4 justify-content-between features-item">

              <div class="col-lg-6" data-aos="fade-up" data-aos-delay="100">
                <img src="@/assets/img/features-1.jpg" class="img-fluid" alt="">
              </div>

              <div class="col-lg-5 d-flex align-items-center" data-aos="fade-up" data-aos-delay="200">
                <div class="content">
                  <h3>Corporis temporibus maiores provident</h3>
                  <p>
                    Ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate
                    velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident.
                  </p>
                  <a href="#" class="btn more-btn">Learn More</a>
                </div>
              </div>

            </div><!-- Features Item -->

            <div class="row gy-4 justify-content-between features-item">

              <div class="col-lg-5 d-flex align-items-center order-2 order-lg-1" data-aos="fade-up" data-aos-delay="100">

                <div class="content">
                  <h3>Neque ipsum omnis sapiente quod quia dicta</h3>
                  <p>
                    Quidem qui dolore incidunt aut. In assumenda harum id iusto lorena plasico mares
                  </p>
                  <ul>
                    <li><i class="bi bi-easel flex-shrink-0"></i> Et corporis ea eveniet ducimus.</li>
                    <li><i class="bi bi-patch-check flex-shrink-0"></i> Exercitationem dolorem sapiente.</li>
                    <li><i class="bi bi-brightness-high flex-shrink-0"></i> Veniam quia modi magnam.</li>
                  </ul>
                  <p></p>
                  <a href="#" class="btn more-btn">Learn More</a>
                </div>

              </div>

              <div class="col-lg-6 order-1 order-lg-2" data-aos="fade-up" data-aos-delay="200">
                <img src="@/assets/img/features-2.jpg" class="img-fluid" alt="">
              </div>

            </div><!-- Features Item -->

            </div>
          </section><!-- /Features Details Section -->

          <!-- Services Section -->
          <section id="services" class="services section light-background">
            <!-- Section Title -->
            <div class="container section-title" data-aos="fade-up">
              <h2>Services</h2>
              <p>Necessitatibus eius consequatur ex aliquid fuga eum quidem sint consectetur velit</p>
            </div><!-- End Section Title -->

            <div class="container">

              <div class="row g-5">

                <div class="col-lg-6" data-aos="fade-up" data-aos-delay="100">
                  <div class="service-item item-cyan position-relative">
                    <i class="bi bi-activity icon"></i>
                    <div>
                      <h3>Nesciunt Mete</h3>
                      <p>Provident nihil minus qui consequatur non omnis maiores. Eos accusantium minus dolores iure perferendis tempore et consequatur.</p>
                      <a href="#" class="read-more stretched-link">Learn More <i class="bi bi-arrow-right"></i></a>
                    </div>
                  </div>
                </div><!-- End Service Item -->

                <div class="col-lg-6" data-aos="fade-up" data-aos-delay="200">
                  <div class="service-item item-orange position-relative">
                    <i class="bi bi-broadcast icon"></i>
                    <div>
                      <h3>Eosle Commodi</h3>
                      <p>Ut autem aut autem non a. Sint sint sit facilis nam iusto sint. Libero corrupti neque eum hic non ut nesciunt dolorem.</p>
                      <a href="#" class="read-more stretched-link">Learn More <i class="bi bi-arrow-right"></i></a>
                    </div>
                  </div>
                </div><!-- End Service Item -->

                <div class="col-lg-6" data-aos="fade-up" data-aos-delay="300">
                  <div class="service-item item-teal position-relative">
                    <i class="bi bi-easel icon"></i>
                    <div>
                      <h3>Ledo Markt</h3>
                      <p>Ut excepturi voluptatem nisi sed. Quidem fuga consequatur. Minus ea aut. Vel qui id voluptas adipisci eos earum corrupti.</p>
                      <a href="#" class="read-more stretched-link">Learn More <i class="bi bi-arrow-right"></i></a>
                    </div>
                  </div>
                </div><!-- End Service Item -->

                <div class="col-lg-6" data-aos="fade-up" data-aos-delay="400">
                  <div class="service-item item-red position-relative">
                    <i class="bi bi-bounding-box-circles icon"></i>
                    <div>
                      <h3>Asperiores Commodi</h3>
                      <p>Non et temporibus minus omnis sed dolor esse consequatur. Cupiditate sed error ea fuga sit provident adipisci neque.</p>
                      <a href="#" class="read-more stretched-link">Learn More <i class="bi bi-arrow-right"></i></a>
                    </div>
                  </div>
                </div><!-- End Service Item -->

                <div class="col-lg-6" data-aos="fade-up" data-aos-delay="500">
                  <div class="service-item item-indigo position-relative">
                    <i class="bi bi-calendar4-week icon"></i>
                    <div>
                      <h3>Velit Doloremque.</h3>
                      <p>Cumque et suscipit saepe. Est maiores autem enim facilis ut aut ipsam corporis aut. Sed animi at autem alias eius labore.</p>
                      <a href="#" class="read-more stretched-link">Learn More <i class="bi bi-arrow-right"></i></a>
                    </div>
                  </div>
                </div><!-- End Service Item -->

                <div class="col-lg-6" data-aos="fade-up" data-aos-delay="600">
                  <div class="service-item item-pink position-relative">
                    <i class="bi bi-chat-square-text icon"></i>
                    <div>
                      <h3>Dolori Architecto</h3>
                      <p>Hic molestias ea quibusdam eos. Fugiat enim doloremque aut neque non et debitis iure. Corrupti recusandae ducimus enim.</p>
                      <a href="#" class="read-more stretched-link">Learn More <i class="bi bi-arrow-right"></i></a>
                    </div>
                  </div>
                </div><!-- End Service Item -->

              </div>

            </div>
          </section><!-- /Services Section -->

          <!-- More Features Section -->
          <section id="more-features" class="more-features section">
            <div class="container">

              <div class="row justify-content-around gy-4">

                <div class="col-lg-6 d-flex flex-column justify-content-center order-2 order-lg-1" data-aos="fade-up" data-aos-delay="100">
                  <h3>Enim quis est voluptatibus aliquid consequatur</h3>
                  <p>Esse voluptas cumque vel exercitationem. Reiciendis est hic accusamus. Non ipsam et sed minima temporibus laudantium. Soluta voluptate sed facere corporis dolores excepturi</p>

                  <div class="row">

                    <div class="col-lg-6 icon-box d-flex">
                      <i class="bi bi-easel flex-shrink-0"></i>
                      <div>
                        <h4>Lorem Ipsum</h4>
                        <p>Voluptatum deleniti atque corrupti quos dolores et quas molestias </p>
                      </div>
                    </div><!-- End Icon Box -->

                    <div class="col-lg-6 icon-box d-flex">
                      <i class="bi bi-patch-check flex-shrink-0"></i>
                      <div>
                        <h4>Nemo Enim</h4>
                        <p>At vero eos et accusamus et iusto odio dignissimos ducimus qui blanditiise</p>
                      </div>
                    </div><!-- End Icon Box -->

                    <div class="col-lg-6 icon-box d-flex">
                      <i class="bi bi-brightness-high flex-shrink-0"></i>
                      <div>
                        <h4>Dine Pad</h4>
                        <p>Explicabo est voluptatum asperiores consequatur magnam. Et veritatis odit</p>
                      </div>
                    </div><!-- End Icon Box -->

                    <div class="col-lg-6 icon-box d-flex">
                      <i class="bi bi-brightness-high flex-shrink-0"></i>
                      <div>
                        <h4>Tride clov</h4>
                        <p>Est voluptatem labore deleniti quis a delectus et. Saepe dolorem libero sit</p>
                      </div>
                    </div><!-- End Icon Box -->

                  </div>

                </div>

                <div class="features-image col-lg-5 order-1 order-lg-2" data-aos="fade-up" data-aos-delay="200">
                  <img src="@/assets/img/features-3.jpg" alt="">
                </div>

              </div>

            </div>
          </section><!-- /More Features Section -->

          <!-- Faq Section -->
          <section id="faq" class="faq section">
            <!-- Section Title -->
            <div class="container section-title" data-aos="fade-up">
              <h2>Frequently Asked Questions</h2>
            </div><!-- End Section Title -->

            <div class="container">

              <div class="row justify-content-center">

                <div class="col-lg-10" data-aos="fade-up" data-aos-delay="100">

                  <div class="faq-container">

                    <div class="faq-item faq-active">
                      <h3>Non consectetur a erat nam at lectus urna duis?</h3>
                      <div class="faq-content">
                        <p>Feugiat pretium nibh ipsum consequat. Tempus iaculis urna id volutpat lacus laoreet non curabitur gravida. Venenatis lectus magna fringilla urna porttitor rhoncus dolor purus non.</p>
                      </div>
                      <i class="faq-toggle bi bi-chevron-right"></i>
                    </div><!-- End Faq item-->

                    <div class="faq-item">
                      <h3>Feugiat scelerisque varius morbi enim nunc faucibus?</h3>
                      <div class="faq-content">
                        <p>Dolor sit amet consectetur adipiscing elit pellentesque habitant morbi. Id interdum velit laoreet id donec ultrices. Fringilla phasellus faucibus scelerisque eleifend donec pretium. Est pellentesque elit ullamcorper dignissim. Mauris ultrices eros in cursus turpis massa tincidunt dui.</p>
                      </div>
                      <i class="faq-toggle bi bi-chevron-right"></i>
                    </div><!-- End Faq item-->

                    <div class="faq-item">
                      <h3>Dolor sit amet consectetur adipiscing elit pellentesque?</h3>
                      <div class="faq-content">
                        <p>Eleifend mi in nulla posuere sollicitudin aliquam ultrices sagittis orci. Faucibus pulvinar elementum integer enim. Sem nulla pharetra diam sit amet nisl suscipit. Rutrum tellus pellentesque eu tincidunt. Lectus urna duis convallis convallis tellus. Urna molestie at elementum eu facilisis sed odio morbi quis</p>
                      </div>
                      <i class="faq-toggle bi bi-chevron-right"></i>
                    </div><!-- End Faq item-->

                    <div class="faq-item">
                      <h3>Ac odio tempor orci dapibus. Aliquam eleifend mi in nulla?</h3>
                      <div class="faq-content">
                        <p>Dolor sit amet consectetur adipiscing elit pellentesque habitant morbi. Id interdum velit laoreet id donec ultrices. Fringilla phasellus faucibus scelerisque eleifend donec pretium. Est pellentesque elit ullamcorper dignissim. Mauris ultrices eros in cursus turpis massa tincidunt dui.</p>
                      </div>
                      <i class="faq-toggle bi bi-chevron-right"></i>
                    </div><!-- End Faq item-->

                    <div class="faq-item">
                      <h3>Tempus quam pellentesque nec nam aliquam sem et tortor?</h3>
                      <div class="faq-content">
                        <p>Molestie a iaculis at erat pellentesque adipiscing commodo. Dignissim suspendisse in est ante in. Nunc vel risus commodo viverra maecenas accumsan. Sit amet nisl suscipit adipiscing bibendum est. Purus gravida quis blandit turpis cursus in</p>
                      </div>
                      <i class="faq-toggle bi bi-chevron-right"></i>
                    </div><!-- End Faq item-->

                    <div class="faq-item">
                      <h3>Perspiciatis quod quo quos nulla quo illum ullam?</h3>
                      <div class="faq-content">
                        <p>Enim ea facilis quaerat voluptas quidem et dolorem. Quis et consequatur non sed in suscipit sequi. Distinctio ipsam dolore et.</p>
                      </div>
                      <i class="faq-toggle bi bi-chevron-right"></i>
                    </div><!-- End Faq item-->

                  </div>

                </div><!-- End Faq Column-->

              </div>

            </div>
          </section><!-- /Faq Section -->

          <!-- Testimonials Section -->
          <section id="testimonials" class="testimonials section light-background">
            <!-- Section Title -->
            <div class="container section-title" data-aos="fade-up">
              <h2>Testimonials</h2>
              <p>Necessitatibus eius consequatur ex aliquid fuga eum quidem sint consectetur velit</p>
            </div><!-- End Section Title -->

            <div class="container" data-aos="fade-up" data-aos-delay="100">

              <div class="swiper init-swiper">
                <div class="swiper-wrapper">

                  <div class="swiper-slide">
                    <div class="testimonial-item">
                      <div class="stars">
                        <i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i>
                      </div>
                      <p>
                        Proin iaculis purus consequat sem cure digni ssim donec porttitora entum suscipit rhoncus. Accusantium quam, ultricies eget id, aliquam eget nibh et. Maecen aliquam, risus at semper.
                      </p>
                      <div class="profile mt-auto">
                        <img src="@/assets/img/testimonials/testimonials-1.jpg" class="testimonial-img" alt="">
                        <h3>Saul Goodman</h3>
                        <h4>Ceo &amp; Founder</h4>
                      </div>
                    </div>
                  </div><!-- End testimonial item -->

                  <div class="swiper-slide">
                    <div class="testimonial-item">
                      <div class="stars">
                        <i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i>
                      </div>
                      <p>
                        Export tempor illum tamen malis malis eram quae irure esse labore quem cillum quid cillum eram malis quorum velit fore eram velit sunt aliqua noster fugiat irure amet legam anim culpa.
                      </p>
                      <div class="profile mt-auto">
                        <img src="@/assets/img/testimonials/testimonials-2.jpg" class="testimonial-img" alt="">
                        <h3>Sara Wilsson</h3>
                        <h4>Designer</h4>
                      </div>
                    </div>
                  </div><!-- End testimonial item -->

                  <div class="swiper-slide">
                    <div class="testimonial-item">
                      <div class="stars">
                        <i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i>
                      </div>
                      <p>
                        Enim nisi quem export duis labore cillum quae magna enim sint quorum nulla quem veniam duis minim tempor labore quem eram duis noster aute amet eram fore quis sint minim.
                      </p>
                      <div class="profile mt-auto">
                        <img src="@/assets/img/testimonials/testimonials-3.jpg" class="testimonial-img" alt="">
                        <h3>Jena Karlis</h3>
                        <h4>Store Owner</h4>
                      </div>
                    </div>
                  </div><!-- End testimonial item -->

                  <div class="swiper-slide">
                    <div class="testimonial-item">
                      <div class="stars">
                        <i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i>
                      </div>
                      <p>
                        Fugiat enim eram quae cillum dolore dolor amet nulla culpa multos export minim fugiat minim velit minim dolor enim duis veniam ipsum anim magna sunt elit fore quem dolore labore illum veniam.
                      </p>
                      <div class="profile mt-auto">
                        <img src="@/assets/img/testimonials/testimonials-4.jpg" class="testimonial-img" alt="">
                        <h3>Matt Brandon</h3>
                        <h4>Freelancer</h4>
                      </div>
                    </div>
                  </div><!-- End testimonial item -->

                  <div class="swiper-slide">
                    <div class="testimonial-item">
                      <div class="stars">
                        <i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i><i class="bi bi-star-fill"></i>
                      </div>
                      <p>
                        Quis quorum aliqua sint quem legam fore sunt eram irure aliqua veniam tempor noster veniam enim culpa labore duis sunt culpa nulla illum cillum fugiat legam esse veniam culpa fore nisi cillum quid.
                      </p>
                      <div class="profile mt-auto">
                        <img src="@/assets/img/testimonials/testimonials-5.jpg" class="testimonial-img" alt="">
                        <h3>John Larson</h3>
                        <h4>Entrepreneur</h4>
                      </div>
                    </div>
                  </div><!-- End testimonial item -->

                </div>
                <div class="swiper-pagination"></div>
              </div>

            </div>
          </section><!-- /Testimonials Section -->

          <!-- Contact Section -->
          <section id="contact" class="contact section">
            <!-- Section Title -->
            <div class="container section-title" data-aos="fade-up">
              <h2>Contact</h2>
              <p>Necessitatibus eius consequatur ex aliquid fuga eum quidem sint consectetur velit</p>
            </div><!-- End Section Title -->

            <div class="container" data-aos="fade-up" data-aos-delay="100">

              <div class="row gy-4">

                <div class="col-lg-6">
                  <div class="info-item d-flex flex-column justify-content-center align-items-center" data-aos="fade-up" data-aos-delay="200">
                    <i class="bi bi-geo-alt"></i>
                    <h3>Address</h3>
                    <p>A108 Adam Street, New York, NY 535022</p>
                  </div>
                </div><!-- End Info Item -->

                <div class="col-lg-3 col-md-6">
                  <div class="info-item d-flex flex-column justify-content-center align-items-center" data-aos="fade-up" data-aos-delay="300">
                    <i class="bi bi-telephone"></i>
                    <h3>Call Us</h3>
                    <p>+1 5589 55488 55</p>
                  </div>
                </div><!-- End Info Item -->

                <div class="col-lg-3 col-md-6">
                  <div class="info-item d-flex flex-column justify-content-center align-items-center" data-aos="fade-up" data-aos-delay="400">
                    <i class="bi bi-envelope"></i>
                    <h3>Email Us</h3>
                    <p>info@example.com</p>
                  </div>
                </div><!-- End Info Item -->

              </div>

              <div class="row gy-4 mt-1">
                <div class="col-lg-6" data-aos="fade-up" data-aos-delay="300">
                  <iframe src="https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d48389.78314118045!2d-74.006138!3d40.710059!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x89c25a22a3bda30d%3A0xb89d1fe6bc499443!2sDowntown%20Conference%20Center!5e0!3m2!1sen!2sus!4v1676961268712!5m2!1sen!2sus" frameborder="0" style="border:0; width: 100%; height: 400px;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
                </div> <!--End Google Maps -->

                <div class="col-lg-6">
                  <form action="#" method="post" class="php-email-form" data-aos="fade-up" data-aos-delay="400">
                    <div class="row gy-4">

                      <div class="col-md-6">
                        <input type="text" name="name" class="form-control" placeholder="Your Name" required="">
                      </div>

                      <div class="col-md-6 ">
                        <input type="email" class="form-control" name="email" placeholder="Your Email" required="">
                      </div>

                      <div class="col-md-12">
                        <input type="text" class="form-control" name="subject" placeholder="Subject" required="">
                      </div>

                      <div class="col-md-12">
                        <textarea class="form-control" name="message" rows="6" placeholder="Message" required=""></textarea>
                      </div>

                      <div class="col-md-12 text-center">
                        <div class="loading">Loading</div>
                        <div class="error-message"></div>
                        <div class="sent-message">Your message has been sent. Thank you!</div>

                        <button type="submit">Send Message</button>
                      </div>

                    </div>
                  </form>
                </div><!-- End Contact Form -->

              </div>

            </div>
          </section><!-- /Contact Section -->
        </main> 

        <AppFooter />

        <BackToTop />
      </div>
    </template> 
    <template #fallback>
      <div>
        <PageLoader :start="true" />
      </div>
    </template>
  </Suspense>
</template>

<style scoped>
.skills {
  padding: 60px 0;
}

.skills .section-title {
  text-align: center;
  padding-bottom: 60px;
  position: relative;
}

.skills .section-title h2 {
  font-size: 32px;
  font-weight: 700;
  margin-bottom: 20px;
  padding-bottom: 20px;
  position: relative;
}

.skills .section-title h2:after {
  content: "";
  position: absolute;
  display: block;
  width: 50px;
  height: 3px;
  background: var(--accent-color);
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
}
  
.skills .section-title p {
  margin-bottom: 0;
}

.skill-category {
  text-align: center;
  margin-bottom: 30px;
}

.skill-category h4 {
  margin-bottom: 20px;
}

.skill-icons {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.skill-icon {
  width: 60px;
  height: 60px;
  margin: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.skill-icon img {
  max-width: 100%;
  max-height: 100%;
  transition: 0.3s;
  opacity: 0.7;
  filter: grayscale(100);
}

.skill-icon img:hover {
  filter: none;
  opacity: 1;
}

@media (max-width: 768px) {
  .skill-icon {
    width: 50px;
    height: 50px;
    margin: 8px;
  }
}
</style>
