<script setup>
import { onMounted } from "vue";

onMounted(() => {
    const scrollTop = document.querySelector('.scroll-top');

    /**
     * Shows or hides the scroll-to-top button based on scroll position
     */
    function toggleScrollTop() {
        if (scrollTop) {
            window.scrollY > 100 ? scrollTop.classList.add('active') : scrollTop.classList.remove('active');
        }
    }

    /**
     * Adds click event listeners to the scroll-to-top button
     * Scrolls to the top of the page when the button is clicked
     */
    if (scrollTop) {
        scrollTop.addEventListener('click', (e) => {
        e.preventDefault();
        window.scrollTo({
            top: 0,
            behavior: 'smooth'
        });
        });
    }

    /**
     * Adds event listeners to toggle the scroll-to-top button based on scroll position
     */
    window.addEventListener('load', toggleScrollTop);
    document.addEventListener('scroll', toggleScrollTop);
});
</script>

<template>
    <!-- Scroll Top -->
    <a href="#" id="scroll-top" class="scroll-top d-flex align-items-center justify-content-center"><i class="bi bi-arrow-up-short"></i></a>
</template>  

<style scoped>
</style>