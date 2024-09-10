<script setup>
import { onMounted, ref } from "vue";

const mobileNavToggleBtn = ref(null);

onMounted(() => {
  mobileNavToggleBtn.value = document.querySelector('.mobile-nav-toggle');

  /**
   * Toggles the 'scrolled' class on the body element based on scroll position
   * This is used for styling changes when the page is scrolled
   */
  function toggleScrolled() {
    const selectBody = document.querySelector('body');
    const selectHeader = document.querySelector('#header');
    if (!selectHeader.classList.contains('scroll-up-sticky') && !selectHeader.classList.contains('sticky-top') && !selectHeader.classList.contains('fixed-top')) return;
    window.scrollY > 100 ? selectBody.classList.add('scrolled') : selectBody.classList.remove('scrolled');
  }

  /**
   * Toggles the mobile navigation menu
   * This function is called when the mobile nav toggle button is clicked
   */
  function mobileNavToogle() {
    document.querySelector('body').classList.toggle('mobile-nav-active');
    mobileNavToggleBtn.value.classList.toggle('bi-list');
    mobileNavToggleBtn.value.classList.toggle('bi-x');
  }

  /**
   * Implements a scrollspy functionality for the navigation menu
   * Highlights the active menu item based on the current scroll position
   */
  function navmenuScrollspy() {
    let navmenulinks = document.querySelectorAll('.navmenu a');
    navmenulinks.forEach(navmenulink => {
      if (!navmenulink.hash) return;
      let section = document.querySelector(navmenulink.hash);
      if (!section) return;
      let position = window.scrollY + 200;
      if (position >= section.offsetTop && position <= (section.offsetTop + section.offsetHeight)) {
        document.querySelectorAll('.navmenu a.active').forEach(link => link.classList.remove('active'));
        navmenulink.classList.add('active');
      } else {
        navmenulink.classList.remove('active');
      }
    });
  }

  // Event Listeners
  document.addEventListener('scroll', toggleScrolled);
  window.addEventListener('load', toggleScrolled);

  if (mobileNavToggleBtn.value) {
    mobileNavToggleBtn.value.addEventListener('click', mobileNavToogle);
  }

  /**
   * Adds click event listeners to navigation menu items
   * Closes the mobile navigation menu when a menu item is clicked
   */
  document.querySelectorAll('#navmenu a').forEach(navmenu => {
    navmenu.addEventListener('click', () => {
      if (document.querySelector('.mobile-nav-active')) {
        mobileNavToogle();
      }
    });
  });

  /**
   * Adds click event listeners to dropdown toggle buttons
   * Toggles the dropdown menu and its active state
   */
  document.querySelectorAll('.navmenu .toggle-dropdown').forEach(navmenu => {
    navmenu.addEventListener('click', function(e) {
      e.preventDefault();
      this.parentNode.classList.toggle('active');
      this.parentNode.nextElementSibling.classList.toggle('dropdown-active');
      e.stopImmediatePropagation();
    });
  });

  window.addEventListener('load', navmenuScrollspy);
  document.addEventListener('scroll', navmenuScrollspy);
});
</script>

<template>
    <header id="header" class="header d-flex align-items-center fixed-top">
        <div class="container-fluid container-xl position-relative d-flex align-items-center">
        <a href="#" class="logo d-flex align-items-center me-auto">
            <img src="@/assets/img/logo.png" alt="logo" loading="lazy" width="30" height="30"/>
            <h1 class="sitename">JA.</h1>
        </a>

        <nav id="navmenu" class="navmenu">
            <ul>
            <li><a href="#" class="active">Home</a></li>
            <li><a href="#">About Me</a></li>
            <li><a href="#">Projects</a></li>
            <li class="dropdown"><a href="#"><span>Dropdown</span> <i class="bi bi-chevron-down toggle-dropdown"></i></a>
                <ul>
                <li><a href="#">Dropdown 1</a></li>
                <li><a href="#">Dropdown 2</a></li>
                <li class="dropdown"><a href="#"><span>Deep Dropdown</span> <i class="bi bi-chevron-down toggle-dropdown"></i></a>
                    <ul>
                    <li><a href="#">Deep Dropdown 1</a></li>
                    <li><a href="#">Deep Dropdown 2</a></li>
                    <li><a href="#">Deep Dropdown 3</a></li>
                    <li><a href="#">Deep Dropdown 4</a></li>
                    <li><a href="#">Deep Dropdown 5</a></li>
                    </ul>
                </li>
                </ul>
            </li>
            <li><a href="#">Contact</a></li>
            </ul>
            <i class="mobile-nav-toggle d-xl-none bi bi-list" ref="mobileNavToggleBtn"></i>
        </nav>
        <a class="btn-get-in-touch" href="#">Get in Touch</a>
        </div>
  </header>
</template>

<style scoped>
</style>