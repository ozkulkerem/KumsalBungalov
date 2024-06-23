<template>
    <section class="whyus">
        <h2>Neden Biz?</h2>
        <!-- <p>Benzersiz deneyime hazır mısın?</p> -->
        <p>
            Doğaya bu kadar yakın olmak ve Kaş'a sadece kısa bir sürüş mesafesinde olmak çok sevildi.
        </p>

        <div class="props">
            <div class="prop">
                <img src="/whyus/Forest-pana.svg" alt="" />
                <div class="overlay">
                    <h3>Doğanın Cenneti</h3>
                    <p>
                        Hemen yanı başınızdaki yürüyüş parkurları ve doğal noktalarla kendinizi doğanın güzelliğine
                        bırakın kapınızın önünde.
                    </p>
                </div>
            </div>

            <div class="prop">
                <img src="/whyus/Sunset-bro.svg" alt="" />
                <div class="overlay">
                    <h3>Kaş Plajlarına Yakın</h3>
                    <p>
                        Kaputaş ve Patara gibi Kaş'ın ünlü plajlarını sadece kısa bir sürüş mesafesinde ziyaret edin.
                    </p>
                </div>
            </div>

            <div class="prop">
                <img src="/whyus/Early morning-bro.svg" alt="" />
                <div class="overlay">
                    <h3>Konfor ve Huzur</h3>
                    <p>
                        Bungalovlarımız konfor için tasarlanmıştır ve koşuşturmadan huzurlu bir kaçış sunar.
                    </p>
                </div>
            </div>

            <div class="prop">
                <img src="/whyus/Athens-bro.svg" alt="" />
                <div class="overlay">
                    <h3>Yerel Gezilecek Yerler</h3>
                    <p>
                        Antik kalıntılardan büyüleyici yerel yapılara kadar Kaş'ın zengin tarihini ve kültürünü
                        keşfedin.
                    </p>
                </div>
            </div>

        </div>
    </section>
</template>

<style scoped>
.whyus {
    position: relative;
    padding: 120px 150px 20px;
    background: rgb(206, 245, 223);
}

.whyus h2 {
    font-size: clamp(2rem, 6vw, 3rem);
    color: #000;
    margin: 60px 0 40px;
    text-align: center;
}

.whyus p {
    font-size: clamp(1rem, 6vw, 1.3rem);
    color: #000;
    font-weight: 400;
    margin-bottom: 30px;
    text-align: center;
    line-height: 1.5;
}

.props {
    display: grid;
    align-items: center;
    justify-items: center;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 40px;
    padding: 60px 60px;
    background: rgb(206, 245, 223);
}

.prop {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    background-color: #fff;
    box-shadow: 0 6px 30px rgba(0, 0, 0, 0.3);
    border-radius: 20px;
    padding: 30px 40px;
    transform-style: preserve-3d;
    -webkit-transform-style: preserve-3d;
    /* Safari ve iOS */
}

.prop img {
    display: block;
    width: 100%;
    max-width: 250px;
    aspect-ratio: 1/1;
    margin: 20px;
}

.prop h3 {
    font-size: 1.4rem;
    font-weight: 700;
    margin: 20px 0 20px;
    text-align: center;
    color: #000;
}

.prop p {
    font-size: 1rem;
    text-align: justify;
    line-height: 1.5;
    color: #000;
}

.overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: linear-gradient(to bottom, rgba(206, 245, 223, 0.9), rgba(164, 209, 198, 0.9), rgba(128, 173, 172, 0.9), rgba(72, 161, 170, 0.9));
    border-radius: 20px;
    list-style: none;
    z-index: 1;
    opacity: 0;
    transform: rotateY(0deg);
    transition: all 0.4s ease-in-out;
    backface-visibility: hidden;
    -webkit-backface-visibility: hidden;
    /* Safari ve iOS */
}

.overlay p {
    padding-left: 5%;
    padding-right: 5%;
}

.prop:hover .overlay {
    opacity: 1;
    transform: rotateY(0deg);
    transition: opacity 0.5s ease-in-out, transform 0.5s ease-in-out;
}

@keyframes flip {
    0% {
        opacity: 1;
        transform: rotateY(0deg);
    }

    50% {
        opacity: 0;
        transform: rotateY(90deg);
    }

    100% {
        opacity: 1;
        transform: rotateY(0deg);
    }
}

@-webkit-keyframes flip {

    /* Safari ve iOS */
    0% {
        opacity: 1;
        -webkit-transform: rotateY(0deg);
    }

    50% {
        opacity: 0;
        -webkit-transform: rotateY(90deg);
    }

    100% {
        opacity: 1;
        -webkit-transform: rotateY(0deg);
    }
}

@media (max-width: 600px) {
    .whyus {
        padding: 70px 0px 0px;
    }

    .props {
        padding: 30px 20px;
        grid-template-columns: 1fr;
    }

    .prop {
        width: 100%;
        max-width: 300px;
    }

    .prop img {
        max-width: 200px;
    }
}
</style>