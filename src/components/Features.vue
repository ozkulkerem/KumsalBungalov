<template>
    <div class="bungalow-features">
        <p>📞 <a href="tel:05302500754">0530 250 0754</a></p>
        <p>📞 <a href="https://www.instagram.com/kumsalbungalov/">İnstagram : kumsalbungalov</a></p>
        <p>📍 Kasaba/Kaş (15 dk 🚘)</p>
        <ul class="feature-list">
            <li>🏡 2+1</li>
            <li>📊 2-4 kişilik</li>
            <li>🏊‍♀️ Havuzlu</li>
            <li>🌳 Müstakil Bahçe</li>
            <li>🍖 Barbekü</li>
            <li>🚘 Otopark</li>
            <li>🛜 Ücretsiz Wifi</li>
        </ul>
    </div>

</template>

<style>
.bungalow-features {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

.feature-list {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    padding: 0;
}

.feature-list li {
    list-style-type: none;
    margin-right: 20px;
}

.bungalow-features p {
    font-size: clamp(1rem, 6vw, 1.3rem);
    color: #000;
    font-weight: 400;
    text-align: center;
    line-height: 1.5;
    padding-top: 5px;
}
</style>