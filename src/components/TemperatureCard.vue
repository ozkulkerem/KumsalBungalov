<template>
    <div class="box">
        <div class="wave -one"></div>
        <div class="wave -two"></div>
        <div class="wave -three"></div>
        <div class="weathercon">
            <i :class="weatherIcon" :style="{ color: fontColor }"></i>
        </div>
        <div class="info">
            <h2 class="location">KAŞ</h2>
            <p class="date">{{ formattedDateTr }}</p>
            <p class="date">{{ formattedDateEn }}</p>
            <h1 class="temp">{{ temperature }}</h1>
        </div>
    </div>
</template>


<script>
export default {
    data() {
        return {
            temperature: '',
            formattedDateTr: '',
            formattedDateEn: '',
            weatherIcon: 'fa fa-sun-o',
            fontColor: '#d36326',
            bgColor: '#eff3f9',
        };
    },
    mounted() {
        this.getWeather();
    },
    methods: {
        async getWeather() {
            const location = 'Kaş'; // Kaş bölgesinin adı
            try {
                const response = await fetch(`https://wttr.in/${location}?format=j1`);
                if (!response.ok) {
                    throw new Error(`API request failed with status ${response.status}`);
                }
                const data = await response.json();
                this.display(data);
            } catch (error) {
                console.error('Error fetching weather data:', error);
                this.temperature = 'N/A';
                this.formattedDateTr = 'N/A';
                this.formattedDateEn = 'N/A';
                this.weatherIcon = 'fa fa-exclamation-triangle';
                this.fontColor = '#ff0000';
            }
        },
        display(data) {
            const weather = data.current_condition[0];
            this.temperature = `${Math.round(weather.temp_C)}°C | ${Math.round(weather.temp_F)}°F`;

            const date = new Date();
            const monthsEn = [
                'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'
            ];
            const weekdaysEn = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];

            const monthsTr = [
                'Ocak', 'Şubat', 'Mart', 'Nisan', 'Mayıs', 'Haziran', 'Temmuz', 'Ağustos', 'Eylül', 'Ekim', 'Kasım', 'Aralık'
            ];
            const weekdaysTr = ['Pazar', 'Pazartesi', 'Salı', 'Çarşamba', 'Perşembe', 'Cuma', 'Cumartesi'];

            const minutes = date.getMinutes() < 10 ? '0' + date.getMinutes() : date.getMinutes();

            this.formattedDateEn = `${weekdaysEn[date.getDay()].toUpperCase()} | ${monthsEn[date.getMonth()].toUpperCase().substring(0, 3)} ${date.getDate()} | ${date.getHours()}:${minutes}`;
            this.formattedDateTr = `${weekdaysTr[date.getDay()].toUpperCase()}  | ${monthsTr[date.getMonth()].toUpperCase()} ${date.getDate()} | ${date.getHours()}:${minutes}`;

            if (Math.round(weather.temp_C) > 25) {
                this.fontColor = '#d36326';
                this.bgColor = '#f3f5d2';
            } else {
                this.fontColor = '#44c3de';
                this.bgColor = '#eff3f9';
            }

            switch (weather.weatherDesc[0].value.toLowerCase()) {
                case 'sunny':
                    this.weatherIcon = 'fa fa-sun-o';
                    break;
                case 'partly cloudy':
                case 'cloudy':
                    this.weatherIcon = 'fa fa-cloud';
                    break;
                case 'rain':
                case 'light rain':
                    this.weatherIcon = 'fa fa-tint';
                    break;
                case 'snow':
                    this.weatherIcon = 'fa fa-snowflake-o';
                    break;
                default:
                    this.weatherIcon = 'fa fa-sun-o';
            }
        }
    },
    watch: {
        bgColor(newColor) {
            document.querySelector('.box').style.background = newColor;
        }
    }
};
</script>

<style scoped>
.box {

    width: 100%;
    border-radius: 5px;
    box-shadow: 0 2px 30px rgba(0, 0, 0, 0.2);
    background: #f6f0e7 !important;
    position: relative;
    overflow: hidden;
    transform: translate3d(0, 0, 0);
    min-height: 250px;
    position: absolute;
    z-index: 99;
}

.wave {
    opacity: 0.3;
    position: absolute;
    top: 120%;
    left: 50%;
    background: white;
    width: 500px;
    height: 500px;
    margin-left: -250px;
    margin-top: -250px;
    transform-origin: 50% 48%;
    border-radius: 43%;
    animation: drift 3000ms infinite linear;
    z-index: 1;
}

.wave.-three {
    animation: drift 5000ms infinite linear;
    z-index: 2 !important;
    opacity: 0.2;
}

.wave.-two {
    animation: drift 7000ms infinite linear;
    opacity: 0.1;
    z-index: 3 !important;
}

.box:after {
    content: "";
    display: block;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    z-index: 11;
    transform: translate3d(0, 0, 0);
}

@keyframes drift {
    from {
        transform: rotate(0deg);
    }

    from {
        transform: rotate(360deg);
    }
}

.info {
    position: absolute;
    bottom: 0;
    width: 100%;
    height: 65%;
    z-index: 4;
}

.location {
    text-align: center;
    font-weight: 800;
}

.date {
    text-align: center;
    margin-top: 5%;
    color: lighten(#000, 10%);
    font-size: 80%;
}

.temp {
    margin-top: 10%;
    text-align: center;
}

.weathercon {
    height: 55%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 3em;
}

@media (max-width: 600px) {
    .wave {
        top: 85%;
    }

    .weathercon {
        font-size: 5em;
    }

    .info {
        font-size: 1.5rem;
    }
}

@media (max-height: 500px) {
    .wave {
        top: 115%;
    }
}

body>span {
    width: 100vw;
    text-align: center;
    color: grey;
}
</style>
