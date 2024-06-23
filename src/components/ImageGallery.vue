<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const count = ref(0);

let gallery = null;
let track = null;
let cards = [];
const easing = 0.05;
let startY = 0;
let endY = 0;
let raf;

const lerp = (start, end, t) => start * (1 - t) + end * t;

function updateScroll() {
    startY = lerp(startY, endY, easing);
    gallery.style.height = `${track.clientHeight}px`;
    track.style.transform = `translateY(-${startY}px)`;
    activateParallax();
    raf = requestAnimationFrame(updateScroll);
    if (startY.toFixed(1) === window.scrollY.toFixed(1)) cancelAnimationFrame(raf);
}

function startScroll() {
    endY = window.scrollY;
    cancelAnimationFrame(raf);
    raf = requestAnimationFrame(updateScroll);
}

function parallax(card) {
    // const wrapper = card.querySelector('.card-image-wrapper');
    // const diff = card.offsetHeight - wrapper.offsetHeight;
    // const { top } = card.getBoundingClientRect();
    // const progress = top / window.innerHeight;
    // const yPos = diff * progress;
    // wrapper.style.transform = `translateY(${yPos}px)`;

    const wrapper = card.querySelector('.card-image-wrapper');
    const gallery = document.querySelector('.gallery');
    const cardRect = card.getBoundingClientRect();
    const galleryRect = gallery.getBoundingClientRect();
    const diff = card.offsetHeight - wrapper.offsetHeight;
    const { top } = cardRect;
    const progress = top / window.innerHeight;
    let yPos = diff * progress;

    // Ensure the parallax effect does not exceed the gallery bounds
    const maxYPos = galleryRect.bottom - cardRect.bottom;
    const minYPos = galleryRect.top - cardRect.top;

    // Adjust yPos to ensure it doesn't go beyond the gallery div boundaries
    yPos = Math.min(Math.max(yPos, minYPos), maxYPos);

    // Check that the bottom of the card does not extend below the gallery div
    const cardBottom = cardRect.bottom + yPos;
    if (cardBottom > galleryRect.bottom) {
        yPos = galleryRect.bottom - cardRect.bottom;
    }

    // Check that the top of the card does not extend above the gallery div
    const cardTop = cardRect.top + yPos;
    if (cardTop < galleryRect.top) {
        yPos = galleryRect.top - cardRect.top;
    }

    wrapper.style.transform = `translateY(${yPos}px)`;
}

const activateParallax = () => cards.forEach(parallax);

function init() {
    activateParallax();
    startScroll();
}

onMounted(() => {
    gallery = document.querySelector('.gallery');
    track = document.querySelector('.gallery-track');
    cards = document.querySelectorAll('.card');

    window.addEventListener('load', updateScroll, false);
    window.addEventListener('scroll', init, false);
    window.addEventListener('resize', updateScroll, false);
});

onBeforeUnmount(() => {
    window.removeEventListener('load', updateScroll, false);
    window.removeEventListener('scroll', init, false);
    window.removeEventListener('resize', updateScroll, false);
});
</script>

<template>
    <div class='gallery'>
        <div class='gallery-track'>
            <div v-for="n in 13" :key="n" class='card'>
                <div class='card-image-wrapper'>
                    <img :src="`/KumsalBungalov/gallery/${n}.jpg`" :alt="`Gallery image ${n}`">
                </div>
            </div>
        </div>
    </div>
</template>


<style scoped>
.gallery {
    margin-bottom: 125px;
    overflow: hidden;
}

.gallery-track {
    position: fixed;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 0.25rem;
    padding: 0.25rem;
    will-change: transform;
}

.card {
    height: 400px;
    overflow: hidden;

    & .card-image-wrapper {
        height: 135%;
        will-change: transform;

        & img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
    }
}

@media (width < 800px) {
    .gallery-track {
        grid-template-columns: repeat(2, 1fr);
    }
}

@media (width < 550px) {
    .gallery-track {
        grid-template-columns: repeat(1, 1fr);
    }
}
</style>