<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
defineProps({
    msg: String,
})

const count = ref(0)

const handleScroll = () => {
    const parallaxElements = document.querySelectorAll('.parallax img');
    const scrollY = window.scrollY;

    parallaxElements.forEach(el => {
        const speed = el.getAttribute('data-speed');
        const yPos = -(scrollY * speed / 300);
        const xPos = -(scrollY * speed / 100);
        // el.style.transform = `translate3d(0px, ${yPos}px, 0px)`;
        if (el.id.includes("right")) {
            el.style.transform = `translate3d(${-xPos}px, ${yPos}px, 0px)`;
        } else if (el.id.includes("left")) {
            el.style.transform = `translate3d(${xPos}px, ${yPos}px, 0px)`;
        } else {
            el.style.transform = `translate3d(0px, ${yPos}px, 0px)`;
        }
    });
}

onMounted(() => {
    window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll);
});
</script>

<template>
    <div class="logo-container">
        <div class="logo">
            <img src="/logo.svg" alt="Logo">
        </div>
    </div>
    <div class="first">

        <section class="parallax">

            <img src="/mountains1.png" id="leftmountain" alt="vacation" data-speed="5" />
            <img src="/mountains2.png" id="rightmountain" alt="vacation" data-speed="6" />
            <img src="/bungalov-cartoon.png" id="bungalov" alt="vacation" data-speed="2" />
            <img src="/leftthree.png" class="three" id="leftthree" alt="vacation" data-speed="100" />
            <img src="/rightthree.png" class="three" id="rightthree" alt="vacation" data-speed="108" />
            <img src="/down.png" id="grass" alt="vacation" data-speed="1" />
            <div class="rabbit"></div>
            <div class="bird-container bird-container--one">
                <div class="bird bird--one"></div>
            </div>
            <div class="bird-container bird-container--two">
                <div class="bird bird--two"></div>
            </div>
            <div class="bird-container bird-container--three">
                <div class="bird bird--three"></div>
            </div>
            <div class="bird-container bird-container--four">
                <div class="bird bird--four"></div>
            </div>
        </section>
    </div>

</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Comfortaa:wght@300;400;500;600;700&family=Mooli&display=swap");

.logo-container {
    position: absolute;
    z-index: 99;
}

.logo img {
    max-width: 100%;
    height: auto;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html {
    scroll-behavior: smooth;
}

h1,
h2,
h3 {
    font-family: "Comfortaa", cursive;
}

.first {
    /* min-height: 100dvh; */
    overflow-x: hidden;
    background: #fff;
    font-family: "Mooli", sans-serif;
}

.parallax {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 150dvh;
    background: rgb(206, 245, 223);
    background: radial-gradient(circle,
            rgba(206, 245, 223, 0.4) 34%,
            rgba(206, 245, 223, 1) 68%);
}

.parallax img {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    pointer-events: none;
    transition: transform 0.2s ease-out;
}

#title {
    position: absolute;
    /* top: 13%; */
    /* top: 55%; */
    font-size: clamp(2rem, 6vw, 4rem);
    color: #000;
    z-index: 50;
    bottom: 35%;
}

#title2 {
    position: absolute;
    /* top: 13%; */
    /* top: 55%; */
    font-size: clamp(1rem, 3vw, 2rem);
    color: #000;
    z-index: 50;
    bottom: 25%;
}

#grass {
    z-index: 2;
}

.three {
    height: 100%;
    z-index: 1;
}

.rabbit {
    position: absolute;
    /* Changed from relative to absolute for better control */
    width: 5em;
    height: 3em;
    color: silver;
    background: radial-gradient(circle at 4.2em 1.4em, #333 0.15em, transparent 0.15em),
        /* eye */
        currentColor;
    border-radius: 70% 90% 60% 50%;
    box-shadow: -0.2em 1em 0 -0.75em #333;
    z-index: 3;
    animation: hop 1s linear infinite;
    bottom: 2em;
    /* Adjust the bottom value as needed */
    left: 50%;
    /* Center horizontally */
    transform: translateX(-50%);
    /* Adjust the horizontal alignment */
}

@keyframes hop {
    20% {
        transform: rotate(-10deg) translate(1em, -2em);
        box-shadow: -0.2em 3em 0 -1em #333;
    }

    40% {
        transform: rotate(10deg) translate(3em, -4em);
        box-shadow: -0.2em 3.25em 0 -1.1em #333;
    }

    60%,
    75% {
        transform: rotate(0deg) translate(4em, 0);
        box-shadow: -0.2em 1em 0 -0.75em #333;
    }
}

/* ears */
.rabbit::before {
    content: '';
    position: absolute;
    width: 0.75em;
    height: 2em;
    background-color: currentColor;
    border-radius: 50% 100% 0 0;
    transform: rotate(-30deg);
    top: -1em;
    right: 1em;
    border: 0.1em solid;
    border-color: darkgrey transparent transparent darkgrey;
    box-shadow: -0.5em 0 0 -0.1em;
}

/* tail and legs */
.rabbit::after {
    content: '';
    position: absolute;
    width: 1em;
    height: 1em;
    background-color: currentColor;
    border-radius: 50%;
    left: -0.3em;
    top: 0.5em;
    box-shadow:
        0.5em 1em 0,
        4em 1em 0 -0.2em,
        4em 1em 0 -0.2em;
    animation: kick 1s infinite linear;
}

@keyframes kick {
    40% {
        box-shadow:
            0.5em 2em 0,
            4.2em 1.75em 0 -0.2em,
            4.4em 1.9em 0 -0.2em;
    }
}

@media (max-width: 1700px) {
    .rabbit {
        bottom: 1em;
        /* Adjust as needed */
    }

    .parallax {
        height: 120dvh;
    }
}

@media (max-width: 1300px) {
    header {
        padding: 30px 50px;
    }

    /* #title {
        top: 16%;
    } */

    .parallax {
        height: 100dvh;
    }

    .blog {
        padding: 100px 120px 20px;
    }

    .rabbit {
        bottom: 0.5em;
        /* Adjust as needed */
        width: 4em;
        height: 2.5em;
        background:
            radial-gradient(circle at 3.5em 1.4em,
                #333 0.15em,
                transparent 0.15em),
            /* eye */
            currentColor;
    }

    .rabbit::before {
        width: 0.6em;
        height: 1.6em;
        top: -0.8em;
        right: 0.8em;
    }

    .rabbit::after {
        width: 0.8em;
        height: 0.8em;
        left: -0.25em;
        top: 0.4em;
        box-shadow:
            0.4em 0.8em 0,
            3.2em 0.8em 0 -0.16em,
            3.2em 0.8em 0 -0.16em;
    }

    @keyframes kick {
        40% {
            box-shadow:
                0.5em 2em 0,
                3em 1.75em 0 -0.2em,
                3.2em 1.9em 0 -0.2em;
        }
    }
}

@media (max-width: 900px) {
    .navigation li {
        margin-left: 10px;
    }

    .parallax {
        height: 70dvh;
    }

    /* 
    #title {
        top: 20%;
    } */

    .blog {
        padding: 90px 100px 20px;
    }

    .cards {
        padding: 40px 40px;
    }

    .card h3 {
        margin: 20px 0 20px;
    }

    .rabbit {
        bottom: 0.5em;
        /* Adjust as needed */
        width: 3.5em;
        height: 2em;
        background:
            radial-gradient(circle at 2.7em 1em,
                #333 0.15em,
                transparent 0.15em),
            /* eye */
            currentColor;
    }

    .rabbit::before {
        width: 0.55em;
        height: 1.4em;
        top: -0.7em;
        right: 0.7em;
    }

    .rabbit::after {
        width: 0.7em;
        height: 0.7em;
        left: -0.2em;
        top: 0.35em;
        box-shadow:
            0.35em 0.7em 0,
            2.8em 0.7em 0 -0.14em,
            2.8em 0.7em 0 -0.14em;
    }

    @keyframes kick {
        40% {
            box-shadow:
                0.5em 1.3em 0,
                2.3em 1.2em 0 -0.2em,
                2.8em 1.5em 0 -0.2em;
        }
    }
}

@media (max-width: 600px) {
    .navigation li {
        margin-left: 5px;
    }

    .parallax {
        height: 60dvh;
    }

    header {
        padding: 30px 10px;
    }

    /* 
    #title {
        top: 40%;
    } */

    .blog {
        padding: 90px 40px 20px;
    }

    .blog p {
        font-size: 1rem;
    }

    .card {
        width: min(100%, 450px);
    }

    .card h3 {
        font-size: 1.2rem;
    }

    .card p {
        font-size: 0.85rem;
        text-align: unset;
    }

    /* .rabbit {
        bottom: 0.5em;
        width: 3em;
        height: 1.7em;
        background:
            radial-gradient(circle at 2.3em 0.8em,
                #333 0.15em,
                transparent 0.15em),
            currentColor;
    } */
    .rabbit {
        bottom: 0.8em;
        /* Adjust as needed */
        width: 2em;
        height: 1.13em;
        background:
            radial-gradient(circle at 1.5em 0.5em,
                #333 0.15em,
                transparent 0.15em),
            /* eye */
            currentColor;
    }

    .rabbit::before {
        width: 0.4em;
        height: 0.8em;
        top: -0.5em;
        right: 0.6em;
    }

    .rabbit::after {
        width: 0.6em;
        height: 0.6em;
        left: -0.15em;
        top: 0.3em;
        box-shadow:
            0.1em 0.2em 0,
            0.1em 0.3em 0 -0.12em,
            0.1em 0.4em 0 -0.12em;
    }

    @keyframes kick {
        40% {
            box-shadow:
                0.1em 0.4em 0,
                2em 0.7em 0 -0.2em,
                2.3em 0.8em 0 -0.2em;
        }
    }
}

.bird {
    background-image: url(/bird-cells-colored.svg);
    background-size: auto 100%;
    width: 75px;
    height: 125px;
    /* width: 8.8em;
    height: 12.5em; */
    will-change: background-position;
    -webkit-animation-name: fly-cycle;
    animation-name: fly-cycle;
    -webkit-animation-timing-function: steps(10);
    animation-timing-function: steps(10);
    -webkit-animation-iteration-count: infinite;
    animation-iteration-count: infinite;
    z-index: 3;
}

.bird--one {
    -webkit-animation-duration: 1s;
    animation-duration: 1s;
    -webkit-animation-delay: -0.5s;
    animation-delay: -0.5s;
}

.bird--two {
    -webkit-animation-duration: 0.9s;
    animation-duration: 0.9s;
    -webkit-animation-delay: -0.75s;
    animation-delay: -0.75s;
}

.bird--three {
    -webkit-animation-duration: 1.25s;
    animation-duration: 1.25s;
    -webkit-animation-delay: -0.25s;
    animation-delay: -0.25s;
}

.bird--four {
    -webkit-animation-duration: 1.1s;
    animation-duration: 1.1s;
    -webkit-animation-delay: -0.5s;
    animation-delay: -0.5s;
}

.bird-container {
    position: absolute;
    bottom: 40%;
    left: -7.5vw;
    -webkit-transform: scale(0);
    transform: scale(0);
    will-change: transform;
    -webkit-animation-name: fly-right-one;
    animation-name: fly-right-one;
    -webkit-animation-timing-function: linear;
    animation-timing-function: linear;
    -webkit-animation-iteration-count: infinite;
    animation-iteration-count: infinite;
}

.bird-container--one {
    -webkit-animation-duration: 15s;
    animation-duration: 15s;
    -webkit-animation-delay: 0;
    animation-delay: 0;
}

.bird-container--two {
    -webkit-animation-duration: 16s;
    animation-duration: 16s;
    -webkit-animation-delay: 1s;
    animation-delay: 1s;
}

.bird-container--three {
    -webkit-animation-duration: 14.6s;
    animation-duration: 14.6s;
    -webkit-animation-delay: 9.5s;
    animation-delay: 9.5s;
}

.bird-container--four {
    -webkit-animation-duration: 16s;
    animation-duration: 16s;
    -webkit-animation-delay: 10.25s;
    animation-delay: 10.25s;
}

@-webkit-keyframes fly-cycle {
    100% {
        background-position: -900px 0;
    }
}

@keyframes fly-cycle {
    100% {
        background-position: -900px 0;
    }
}

@-webkit-keyframes fly-right-one {
    0% {
        left: -10%;
        -webkit-transform: scale(0.3);
        transform: scale(0.3);
    }

    10% {
        left: 10%;
        -webkit-transform: translateY(2vh) scale(0.4);
        transform: translateY(2vh) scale(0.4);
    }

    20% {
        left: 30%;
        -webkit-transform: translateY(0vh) scale(0.5);
        transform: translateY(0vh) scale(0.5);
    }

    30% {
        left: 50%;
        -webkit-transform: translateY(4vh) scale(0.6);
        transform: translateY(4vh) scale(0.6);
    }

    40% {
        left: 70%;
        -webkit-transform: translateY(2vh) scale(0.6);
        transform: translateY(2vh) scale(0.6);
    }

    50% {
        left: 90%;
        -webkit-transform: translateY(0vh) scale(0.6);
        transform: translateY(0vh) scale(0.6);
    }

    60% {
        left: 110%;
        -webkit-transform: translateY(0vh) scale(0.6);
        transform: translateY(0vh) scale(0.6);
    }

    100% {
        left: 110%;
        opacity: 1;
        -webkit-transform: translateY(0vh) scale(0.6);
        transform: translateY(0vh) scale(0.6);
    }
}

@keyframes fly-right-one {
    0% {
        left: -10%;
        -webkit-transform: scale(0.3);
        transform: scale(0.3);
    }

    10% {
        left: 10%;
        -webkit-transform: translateY(2vh) scale(0.4);
        transform: translateY(2vh) scale(0.4);
    }

    20% {
        left: 30%;
        -webkit-transform: translateY(0vh) scale(0.5);
        transform: translateY(0vh) scale(0.5);
    }

    30% {
        left: 50%;
        -webkit-transform: translateY(4vh) scale(0.6);
        transform: translateY(4vh) scale(0.6);
    }

    40% {
        left: 70%;
        -webkit-transform: translateY(2vh) scale(0.6);
        transform: translateY(2vh) scale(0.6);
    }

    50% {
        left: 90%;
        -webkit-transform: translateY(0vh) scale(0.6);
        transform: translateY(0vh) scale(0.6);
    }

    60% {
        left: 110%;
        -webkit-transform: translateY(0vh) scale(0.6);
        transform: translateY(0vh) scale(0.6);
    }

    100% {
        left: 110%;
        opacity: 1;
        -webkit-transform: translateY(0vh) scale(0.6);
        transform: translateY(0vh) scale(0.6);
    }
}

@-webkit-keyframes fly-right-two {
    0% {
        left: -10%;
        opacity: 1;
        -webkit-transform: translateY(-2vh) scale(0.5);
        transform: translateY(-2vh) scale(0.5);
    }

    10% {
        left: 10%;
        -webkit-transform: translateY(0vh) scale(0.4);
        transform: translateY(0vh) scale(0.4);
    }

    20% {
        left: 30%;
        -webkit-transform: translateY(-4vh) scale(0.6);
        transform: translateY(-4vh) scale(0.6);
    }

    30% {
        left: 50%;
        -webkit-transform: translateY(1vh) scale(0.45);
        transform: translateY(1vh) scale(0.45);
    }

    40% {
        left: 70%;
        -webkit-transform: translateY(-2.5vh) scale(0.5);
        transform: translateY(-2.5vh) scale(0.5);
    }

    50% {
        left: 90%;
        -webkit-transform: translateY(0vh) scale(0.45);
        transform: translateY(0vh) scale(0.45);
    }

    51% {
        left: 110%;
        -webkit-transform: translateY(0vh) scale(0.45);
        transform: translateY(0vh) scale(0.45);
    }

    100% {
        left: 110%;
        -webkit-transform: translateY(0vh) scale(0.45);
        transform: translateY(0vh) scale(0.45);
    }
}

@keyframes fly-right-two {
    0% {
        left: -10%;
        opacity: 1;
        -webkit-transform: translateY(-2vh) scale(0.5);
        transform: translateY(-2vh) scale(0.5);
    }

    10% {
        left: 10%;
        -webkit-transform: translateY(0vh) scale(0.4);
        transform: translateY(0vh) scale(0.4);
    }

    20% {
        left: 30%;
        -webkit-transform: translateY(-4vh) scale(0.6);
        transform: translateY(-4vh) scale(0.6);
    }

    30% {
        left: 50%;
        -webkit-transform: translateY(1vh) scale(0.45);
        transform: translateY(1vh) scale(0.45);
    }

    40% {
        left: 70%;
        -webkit-transform: translateY(-2.5vh) scale(0.5);
        transform: translateY(-2.5vh) scale(0.5);
    }

    50% {
        left: 90%;
        -webkit-transform: translateY(0vh) scale(0.45);
        transform: translateY(0vh) scale(0.45);
    }

    51% {
        left: 110%;
        -webkit-transform: translateY(0vh) scale(0.45);
        transform: translateY(0vh) scale(0.45);
    }

    100% {
        left: 110%;
        -webkit-transform: translateY(0vh) scale(0.45);
        transform: translateY(0vh) scale(0.45);
    }
}
</style>
