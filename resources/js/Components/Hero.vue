<template>
    <main class="hero">
        <div class="hero-content">
            <div class="hero-image-wrapper">
                <img src="/images/hero-img.png" alt="Пицца от Дениса" class="hero-image" />
            </div>
            <div class="hero-text">
                <h1 class="hero-title">Добро пожаловать!</h1>
                <p class="hero-subtitle">Самая вкусная пицца в городе</p>
                <p class="hero-description">Свежие ингредиенты, традиционные рецепты и быстрая доставка</p>
            </div>
        </div>
    </main>
</template>

<style scoped>
.hero {
    max-width: 1200px;
    margin: 30px auto;
    padding: 0 20px;
}

.hero-content {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 40px;
    background: linear-gradient(135deg, #fffaf4 0%, #f5e6d3 100%);
    border-radius: 24px;
    padding: 40px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
}

.hero-image-wrapper {
    flex-shrink: 0;
}

.hero-image {
    width: 100%;
    max-width: 400px;
    height: auto;
    border-radius: 16px;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
    object-fit: cover;
}

.hero-text {
    flex: 1;
    text-align: left;
}

.hero-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 42px;
    color: #3b2b1f;
    margin: 0 0 16px 0;
    font-weight: bold;
    line-height: 1.2;
}

.hero-subtitle {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 24px;
    color: #99582A;
    margin: 0 0 16px 0;
    font-weight: 600;
}

.hero-description {
    font-size: 18px;
    color: #6a5b4a;
    margin: 0;
    line-height: 1.6;
    max-width: 500px;
}

@media (max-width: 968px) {
    .hero-content {
        flex-direction: column;
        text-align: center;
        padding: 30px 20px;
    }
    
    .hero-text {
        text-align: center;
    }
    
    .hero-title {
        font-size: 32px;
    }
    
    .hero-subtitle {
        font-size: 20px;
    }
    
    .hero-description {
        font-size: 16px;
        max-width: 100%;
    }
    
    .hero-image {
        max-width: 300px;
    }
}

@media (max-width: 480px) {
    .hero {
        margin: 20px auto;
        padding: 0 15px;
    }
    
    .hero-content {
        padding: 20px 15px;
    }
    
    .hero-title {
        font-size: 28px;
    }
    
    .hero-subtitle {
        font-size: 18px;
    }
    
    .hero-description {
        font-size: 14px;
    }
}
</style>
