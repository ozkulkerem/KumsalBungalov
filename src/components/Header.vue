<template>
    <header>
        <div class="container">
            <div class="logo">
                <img src="/logo.svg" alt="Logo">
            </div>
            <div class="contact-info">
                <a href="https://www.instagram.com/yourprofile" target="_blank">
                    <i class="fa fa-instagram" aria-hidden="true"></i>
                </a>
                <p>İletişim: +90 123 456 78 90</p>
            </div>
        </div>
    </header>
</template>

<style scoped>
header {
    background-color: #333;
    color: #fff;
    padding: 10px 0;
}

.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

.logo img {
    height: 50px;
}

.contact-info {
    display: flex;
    align-items: center;
}

.contact-info a {
    margin-right: 10px;
}

.contact-info img {
    height: 30px;
}

.contact-info p {
    margin: 0;
}

/* Responsive Design */
@media (max-width: 768px) {
    .container {
        flex-direction: column;
        align-items: flex-start;
    }

    .logo img {
        margin-bottom: 10px;
    }

    .contact-info {
        flex-direction: column;
        align-items: flex-start;
    }

    .contact-info a {
        margin-bottom: 5px;
    }
}
</style>
