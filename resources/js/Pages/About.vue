<script setup>
import { Head, Link } from '@inertiajs/vue3';
import Header from '@/Components/Header.vue';
import Footer from '@/Components/Footer.vue';
</script>

<template>
    <Head title="О нас - Пицца от Дениса">
        <link rel="preconnect" href="https://fonts.googleapis.com" />
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
        <link href="https://fonts.googleapis.com/css2?family=Dela+Gothic+One&display=swap" rel="stylesheet" />
    </Head>
    
    <div class="min-h-screen bg-cream">
        <Header />
        
        <main class="about-page">
            <section class="hero-section">
                <div class="hero-content">
                    <h1 class="hero-title">О нас</h1>
                    <p class="hero-subtitle">Мы готовим пиццу с любовью уже более 10 лет</p>
                </div>
            </section>

            <section class="content-section">
                <div class="container">
                    <div class="about-grid">
                        <div class="about-card">
                            <div class="card-icon">
                                <svg width="60" height="60" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                    <path d="M12 2L2 7L12 12L22 7L12 2Z" stroke="#B84A3A" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M2 17L12 22L22 17" stroke="#B84A3A" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                                    <path d="M2 12L12 17L22 12" stroke="#B84A3A" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                                </svg>
                            </div>
                            <h3 class="card-title">Свежие ингредиенты</h3>
                            <p class="card-text">Мы используем только свежие и качественные продукты от проверенных поставщиков</p>
                        </div>

                        <div class="about-card">
                            <div class="card-icon">
                                <svg width="60" height="60" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                    <path d="M12 2L15.09 8.26L22 9.27L17 14.14L18.18 21.02L12 17.77L5.82 21.02L7 14.14L2 9.27L8.91 8.26L12 2Z" stroke="#B84A3A" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                                </svg>
                            </div>
                            <h3 class="card-title">Традиционные рецепты</h3>
                            <p class="card-text">Наши рецепты передаются из поколения в поколение и проверены временем</p>
                        </div>

                        <div class="about-card">
                            <div class="card-icon">
                                <svg width="60" height="60" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                    <path d="M12 2C6.48 2 2 6.48 2 12C2 17.52 6.48 22 12 22C17.52 22 22 17.52 22 12C22 6.48 17.52 2 12 2ZM13 17H11V15H13V17ZM13 13H11V7H13V13Z" fill="#B84A3A"/>
                                </svg>
                            </div>
                            <h3 class="card-title">Быстрая доставка</h3>
                            <p class="card-text">Доставляем вашу пиццу горячей и свежей в течение 30-45 минут</p>
                        </div>
                    </div>

                    <div class="story-section">
                        <div class="story-content">
                            <h2 class="section-title">Наша история</h2>
                            <div class="story-text">
                                <p>
                                    "Пицца от Дениса" была основана в 2013 году с простой идеей - готовить самую вкусную пиццу 
                                    из лучших ингредиентов. За годы работы мы стали любимым местом для тысяч клиентов, 
                                    которые ценят качество и традиционный вкус.
                                </p>
                                <p>
                                    Мы гордимся тем, что используем только натуральные продукты, готовим тесто по собственному 
                                    рецепту и всегда рады видеть улыбки наших гостей. Каждая пицца готовится с любовью и вниманием 
                                    к деталям.
                                </p>
                                <p>
                                    Наша команда - это опытные повара, которые знают секреты идеальной пиццы. Мы постоянно 
                                    совершенствуемся и радуем вас новыми вкусами, сохраняя при этом классические рецепты.
                                </p>
                            </div>
                        </div>
                    </div>

                    <div class="values-section">
                        <h2 class="section-title">Наши ценности</h2>
                        <div class="values-grid">
                            <div class="value-item">
                                <h4>Качество</h4>
                                <p>Только лучшие ингредиенты и проверенные рецепты</p>
                            </div>
                            <div class="value-item">
                                <h4>Скорость</h4>
                                <p>Быстрая доставка и приготовление</p>
                            </div>
                            <div class="value-item">
                                <h4>Традиции</h4>
                                <p>Классические рецепты итальянской кухни</p>
                            </div>
                            <div class="value-item">
                                <h4>Забота</h4>
                                <p>Внимание к каждому клиенту</p>
                            </div>
                        </div>
                    </div>

                    <div class="cta-section">
                        <h2 class="cta-title">Попробуйте нашу пиццу!</h2>
                        <p class="cta-text">Закажите прямо сейчас и насладитесь неповторимым вкусом</p>
                        <Link :href="route('welcome')" class="cta-button">
                            Перейти в меню
                        </Link>
                    </div>
                </div>
            </section>
        </main>

        <Footer />
    </div>
</template>

<style scoped>
.bg-cream {
    background-color: #F8F5F0;
}

.about-page {
    min-height: calc(100vh - 200px);
}

.hero-section {
    background: linear-gradient(135deg, #C85D3E 0%, #B84A3A 100%);
    padding: 80px 20px;
    text-align: center;
    border-bottom: 3px solid rgba(168, 61, 46, 0.3);
}

.hero-content {
    max-width: 800px;
    margin: 0 auto;
}

.hero-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 48px;
    color: white;
    margin: 0 0 20px 0;
    font-weight: bold;
}

.hero-subtitle {
    font-size: 24px;
    color: white;
    margin: 0;
    font-weight: 600;
}

.content-section {
    padding: 60px 20px;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
}

.about-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 30px;
    margin-bottom: 80px;
}

.about-card {
    background: white;
    padding: 40px 30px;
    border-radius: 24px;
    text-align: center;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
    transition: all 0.3s ease;
    border: 2px solid transparent;
}

.about-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
    border-color: #C85D3E;
}

.card-icon {
    margin-bottom: 20px;
    display: flex;
    justify-content: center;
}

.card-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 24px;
    color: #3D2E28;
    margin: 0 0 16px 0;
    font-weight: bold;
}

.card-text {
    font-size: 16px;
    color: #6B5A4A;
    line-height: 1.6;
    margin: 0;
}

.story-section {
    margin-bottom: 80px;
}

.section-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 36px;
    color: #3D2E28;
    text-align: center;
    margin: 0 0 40px 0;
    font-weight: bold;
}

.story-content {
    background: linear-gradient(135deg, #F8F5F0 0%, #F5F0E8 100%);
    padding: 40px;
    border-radius: 24px;
    border: 2px solid rgba(232, 221, 208, 0.6);
}

.story-text {
    max-width: 800px;
    margin: 0 auto;
}

.story-text p {
    font-size: 18px;
    color: #3D2E28;
    line-height: 1.8;
    margin: 0 0 20px 0;
}

.story-text p:last-child {
    margin-bottom: 0;
}

.values-section {
    margin-bottom: 80px;
}

.values-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 30px;
}

.value-item {
    background: white;
    padding: 30px;
    border-radius: 20px;
    text-align: center;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
    border: 2px solid rgba(232, 221, 208, 0.6);
    transition: all 0.3s ease;
}

.value-item:hover {
    border-color: #C85D3E;
    transform: translateY(-5px);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.12);
}

.value-item h4 {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 22px;
    color: #B84A3A;
    margin: 0 0 12px 0;
    font-weight: bold;
}

.value-item p {
    font-size: 15px;
    color: #6B5A4A;
    line-height: 1.6;
    margin: 0;
}

.cta-section {
    background: linear-gradient(135deg, #C85D3E 0%, #B84A3A 100%);
    padding: 60px 40px;
    border-radius: 24px;
    text-align: center;
    box-shadow: 0 8px 30px rgba(230, 57, 70, 0.3);
}

.cta-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 36px;
    color: white;
    margin: 0 0 16px 0;
    font-weight: bold;
}

.cta-text {
    font-size: 20px;
    color: white;
    margin: 0 0 30px 0;
    font-weight: 600;
}

.cta-button {
    display: inline-block;
    padding: 16px 40px;
    background: #B84A3A;
    color: white;
    text-decoration: none;
    border-radius: 16px;
    font-family: "Dela Gothic One", sans-serif;
    font-size: 18px;
    font-weight: bold;
    transition: all 0.3s ease;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

.cta-button:hover {
    background: #C1121F;
    transform: translateY(-3px);
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
}

@media (max-width: 968px) {
    .hero-section {
        padding: 70px 20px;
    }
    
    .hero-title {
        font-size: 42px;
    }
    
    .about-grid {
        grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
        gap: 25px;
    }
    
    .values-grid {
        grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
        gap: 25px;
    }
}

@media (max-width: 768px) {
    .hero-section {
        padding: 60px 20px;
    }
    
    .hero-title {
        font-size: 36px;
    }
    
    .hero-subtitle {
        font-size: 20px;
    }
    
    .content-section {
        padding: 40px 15px;
    }
    
    .about-grid {
        grid-template-columns: 1fr;
        gap: 20px;
        margin-bottom: 60px;
    }
    
    .section-title {
        font-size: 28px;
        margin-bottom: 30px;
    }
    
    .story-content {
        padding: 30px 20px;
    }
    
    .story-text p {
        font-size: 16px;
    }
    
    .values-grid {
        grid-template-columns: 1fr;
        gap: 20px;
    }
    
    .cta-section {
        padding: 40px 20px;
    }
    
    .cta-title {
        font-size: 28px;
    }
    
    .cta-text {
        font-size: 18px;
    }
}

@media (max-width: 640px) {
    .hero-section {
        padding: 50px 15px;
    }
    
    .hero-title {
        font-size: 32px;
    }
    
    .hero-subtitle {
        font-size: 18px;
    }
    
    .content-section {
        padding: 35px 12px;
    }
    
    .about-card {
        padding: 30px 20px;
    }
    
    .card-title {
        font-size: 22px;
    }
    
    .card-text {
        font-size: 15px;
    }
    
    .section-title {
        font-size: 24px;
        margin-bottom: 25px;
    }
    
    .story-content {
        padding: 25px 18px;
    }
    
    .story-text p {
        font-size: 15px;
    }
    
    .value-item {
        padding: 25px 20px;
    }
    
    .value-item h4 {
        font-size: 20px;
    }
    
    .cta-section {
        padding: 35px 18px;
    }
    
    .cta-title {
        font-size: 24px;
    }
    
    .cta-text {
        font-size: 16px;
    }
    
    .cta-button {
        padding: 14px 32px;
        font-size: 16px;
    }
}

@media (max-width: 480px) {
    .hero-section {
        padding: 40px 12px;
    }
    
    .hero-title {
        font-size: 28px;
    }
    
    .hero-subtitle {
        font-size: 16px;
    }
    
    .content-section {
        padding: 30px 10px;
    }
    
    .about-card {
        padding: 25px 18px;
    }
    
    .card-icon svg {
        width: 50px;
        height: 50px;
    }
    
    .card-title {
        font-size: 20px;
    }
    
    .section-title {
        font-size: 22px;
    }
    
    .story-content {
        padding: 20px 15px;
    }
    
    .story-text p {
        font-size: 14px;
    }
    
    .value-item {
        padding: 20px 18px;
    }
    
    .cta-section {
        padding: 30px 15px;
    }
    
    .cta-title {
        font-size: 22px;
    }
    
    .cta-text {
        font-size: 15px;
    }
    
    .cta-button {
        padding: 12px 28px;
        font-size: 15px;
    }
}
</style>

