<template>
    <section class="products">
        <h2 class="section-title">Наши пиццы</h2>
        
        <div class="products-grid">
            <div class="card">
                <div class="card-image-wrapper">
                    <div class="placeholder-image">
                        <svg width="80" height="80" viewBox="0 0 80 80" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <circle cx="40" cy="40" r="35" fill="#d7b389" stroke="#c49a6c" stroke-width="2"/>
                            <path d="M40 20 L50 35 L30 35 Z" fill="#99582A"/>
                            <circle cx="40" cy="40" r="8" fill="#c49a6c"/>
                        </svg>
                    </div>
                </div>
                <div class="card-content">
                    <h3 class="card-title">Пицца "4 Сыра"</h3>
                    <p class="card-description">Моцарелла, горгонзола, пармезан, чеддер</p>
                    <div class="sizes">35 см — 1790₽ / 45 см — 2190₽</div>
                    <button class="btn">Добавить в корзину</button>
                </div>
            </div>
    
            <div class="card">
                <div class="card-image-wrapper">
                    <div class="placeholder-image">
                        <svg width="80" height="80" viewBox="0 0 80 80" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <circle cx="40" cy="40" r="35" fill="#d7b389" stroke="#c49a6c" stroke-width="2"/>
                            <path d="M40 20 L50 35 L30 35 Z" fill="#99582A"/>
                            <circle cx="40" cy="40" r="8" fill="#c49a6c"/>
                        </svg>
                    </div>
                </div>
                <div class="card-content">
                    <h3 class="card-title">Классическая пицца</h3>
                    <p class="card-description">Томаты, моцарелла, базилик, орегано</p>
                    <div class="sizes">35 см — 1450₽ / 45 см — 1850₽</div>
                    <button class="btn">Добавить в корзину</button>
                </div>
            </div>

            <div class="card">
                <div class="card-image-wrapper">
                    <div class="placeholder-image">
                        <svg width="80" height="80" viewBox="0 0 80 80" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <circle cx="40" cy="40" r="35" fill="#d7b389" stroke="#c49a6c" stroke-width="2"/>
                            <path d="M40 20 L50 35 L30 35 Z" fill="#99582A"/>
                            <circle cx="40" cy="40" r="8" fill="#c49a6c"/>
                        </svg>
                    </div>
                </div>
                <div class="card-content">
                    <h3 class="card-title">Гавайская</h3>
                    <p class="card-description">Ветчина, ананас, моцарелла, соус</p>
                    <div class="sizes">35 см — 1730₽ / 45 см — 2100₽</div>
                    <button class="btn">Добавить в корзину</button>
                </div>
            </div>

            <div class="card">
                <div class="card-image-wrapper">
                    <div class="placeholder-image">
                        <svg width="80" height="80" viewBox="0 0 80 80" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <circle cx="40" cy="40" r="35" fill="#d7b389" stroke="#c49a6c" stroke-width="2"/>
                            <path d="M40 20 L50 35 L30 35 Z" fill="#99582A"/>
                            <circle cx="40" cy="40" r="8" fill="#c49a6c"/>
                        </svg>
                    </div>
                </div>
                <div class="card-content">
                    <h3 class="card-title">Пепперони</h3>
                    <p class="card-description">Пепперони, моцарелла, томатный соус</p>
                    <div class="sizes">35 см — 1650₽ / 45 см — 2050₽</div>
                    <button class="btn">Добавить в корзину</button>
                </div>
            </div>

            <div class="card">
                <div class="card-image-wrapper">
                    <div class="placeholder-image">
                        <svg width="80" height="80" viewBox="0 0 80 80" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <circle cx="40" cy="40" r="35" fill="#d7b389" stroke="#c49a6c" stroke-width="2"/>
                            <path d="M40 20 L50 35 L30 35 Z" fill="#99582A"/>
                            <circle cx="40" cy="40" r="8" fill="#c49a6c"/>
                        </svg>
                    </div>
                </div>
                <div class="card-content">
                    <h3 class="card-title">Маргарита</h3>
                    <p class="card-description">Моцарелла, томаты, базилик</p>
                    <div class="sizes">35 см — 1350₽ / 45 см — 1750₽</div>
                    <button class="btn">Добавить в корзину</button>
                </div>
            </div>

            <div class="card">
                <div class="card-image-wrapper">
                    <div class="placeholder-image">
                        <svg width="80" height="80" viewBox="0 0 80 80" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <circle cx="40" cy="40" r="35" fill="#d7b389" stroke="#c49a6c" stroke-width="2"/>
                            <path d="M40 20 L50 35 L30 35 Z" fill="#99582A"/>
                            <circle cx="40" cy="40" r="8" fill="#c49a6c"/>
                        </svg>
                    </div>
                </div>
                <div class="card-content">
                    <h3 class="card-title">Мясная</h3>
                    <p class="card-description">Ветчина, бекон, колбаса, моцарелла</p>
                    <div class="sizes">35 см — 1890₽ / 45 см — 2290₽</div>
                    <button class="btn">Добавить в корзину</button>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>
.products {
    max-width: 1200px;
    margin: 40px auto;
    padding: 0 20px;
}

.section-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 32px;
    color: #3b2b1f;
    text-align: center;
    margin-bottom: 40px;
    font-weight: bold;
}

.products-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 30px;
}

.card {
    background: white;
    border-radius: 20px;
    overflow: hidden;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    display: flex;
    flex-direction: column;
}

.card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.card-image-wrapper {
    width: 100%;
    padding-top: 100%;
    position: relative;
    background: linear-gradient(135deg, #fffaf4 0%, #f5e6d3 100%);
}

.placeholder-image {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 60%;
    height: 60%;
}

.card-content {
    padding: 20px;
    display: flex;
    flex-direction: column;
    flex: 1;
}

.card-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 20px;
    color: #3b2b1f;
    margin: 0 0 8px 0;
    font-weight: bold;
}

.card-description {
    font-size: 14px;
    color: #6a5b4a;
    margin: 0 0 12px 0;
    line-height: 1.5;
    flex: 1;
}

.sizes {
    color: #99582A;
    font-size: 14px;
    font-weight: 600;
    margin: 12px 0;
    padding: 8px 0;
    border-top: 1px solid #e8dcc6;
    border-bottom: 1px solid #e8dcc6;
}

.btn {
    margin-top: auto;
    padding: 12px 24px;
    background: #d7b389;
    color: #3b2b1f;
    border: none;
    border-radius: 12px;
    font-weight: bold;
    font-size: 16px;
    font-family: "Dela Gothic One", sans-serif;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 2px 8px rgba(153, 88, 42, 0.2);
}

.btn:hover {
    background: #c49a6c;
    transform: scale(1.02);
    box-shadow: 0 4px 12px rgba(153, 88, 42, 0.3);
}

.btn:active {
    transform: scale(0.98);
}

@media (max-width: 768px) {
    .products {
        margin: 30px auto;
        padding: 0 15px;
    }
    
    .section-title {
        font-size: 24px;
        margin-bottom: 30px;
    }
    
    .products-grid {
        grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
        gap: 20px;
    }
}

@media (max-width: 480px) {
    .products-grid {
        grid-template-columns: 1fr;
    }
}
</style>
