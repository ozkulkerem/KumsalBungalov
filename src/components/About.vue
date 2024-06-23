<script setup>
import ImageGallery from '../components/ImageGallery.vue'
import Features from '../components/Features.vue'
</script>
<template>
    <section class="about">
        <Features></Features>
        <h2>Kumsal Bungalov - Doğanın İçinde Huzuru Yaşayın</h2>

        <p>Benzersiz deneyime hazır mısın?</p>
        <p>
            Doğanın kalbinde yer alan bungalovumuz, görkemli dağlarla çevrili sakin bir sığınak sunmaktadır.
            Kaş merkezine arabayla sadece 15 dakika uzaklıkta bulunan bungalovumuz, inziva ve erişilebilirliğin mükemmel
            bir karışımını sunmaktadır. Keşfedilecek kadar yakınken, doğal çevrenin huzur ve sessizliğinin tadını
            çıkarın 🏝️✨
        </p>
        <ImageGallery></ImageGallery>

        <p>
            Kumsal Bungalov doğanın kalbinde , Dünyanın en güzel palajlarına sahip Kaş'a komşu tatil keyfi! 🏖️
        </p>
    </section>
</template>

<style scoped>
.about {
    position: relative;
    padding: 120px 0px 20px;
    background: #f6f0e7;
}

.about::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 50px;
    background: rgb(246, 240, 231);
    background: radial-gradient(circle,
            rgba(246, 240, 231, 1) 54%,
            rgba(0, 114, 125, 1) 99%);
    z-index: 999;
}

.about h2 {
    font-size: clamp(2rem, 6vw, 3rem);
    color: #000;
    margin: 60px 0 40px;
    text-align: center;
}

.about p {
    font-size: clamp(1rem, 6vw, 1.3rem);
    color: #000;
    font-weight: 400;
    text-align: center;
    line-height: 1.5;
    padding: 20px 50px 30px 50px;
}

@media (max-width: 600px) {
    .about {
        padding: 120px 0px 0px;
    }

}
</style>
