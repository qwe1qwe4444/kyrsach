<script setup>
import { Head, Link } from '@inertiajs/vue3';
import { ref, computed, onMounted } from 'vue';
import Header from '@/Components/Header.vue';
import Footer from '@/Components/Footer.vue';

const cart = ref([]);

const loadCart = () => {
    const savedCart = localStorage.getItem('cart');
    if (savedCart) {
        try {
            cart.value = JSON.parse(savedCart);
        } catch (e) {
            cart.value = [];
        }
    }
};

const removeFromCart = (index) => {
    cart.value.splice(index, 1);
    localStorage.setItem('cart', JSON.stringify(cart.value));
};

const updateCartItemQuantity = (index, quantity) => {
    if (quantity <= 0) {
        removeFromCart(index);
    } else {
        cart.value[index].quantity = quantity;
        localStorage.setItem('cart', JSON.stringify(cart.value));
    }
};

const clearCart = () => {
    cart.value = [];
    localStorage.removeItem('cart');
};

onMounted(() => {
    loadCart();
});

const totalPrice = computed(() => {
    return cart.value.reduce((sum, item) => sum + (item.price * item.quantity), 0);
});

const handleCheckout = () => {
    alert('Спасибо за заказ! Мы свяжемся с вами для подтверждения.');
    clearCart();
};

const handleImageError = (event) => {
    event.target.src = 'data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAwIiBoZWlnaHQ9IjQwMCIgdmlld0JveD0iMCAwIDgwIDgwIiBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPjxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNDAwIiBmaWxsPSIjZjVmNTVmNSIvPjxjaXJjbGUgY3g9IjIwMCIgY3k9IjIwMCIgcj0iMTUwIiBmaWxsPSIjZDdiMzg5IiBzdHJva2U9IiNjNDlhNmMiIHN0cm9rZS13aWR0aD0iNCIvPjxwYXRoIGQ9Ik0yMDAgMTAwIEwyNTAgMTc1IEwxNTAgMTc1IFoiIGZpbGw9IiM5OTU4MkEiLz48Y2lyY2xlIGN4PSIyMDAiIGN5PSIyMDAiIHI9IjQwIiBmaWxsPSIjYzQ5YTZjIi8+PC9zdmc+';
};
</script>

<template>
    <Head title="Корзина - Пицца от Дениса">
        <link rel="preconnect" href="https://fonts.googleapis.com" />
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
        <link href="https://fonts.googleapis.com/css2?family=Dela+Gothic+One&display=swap" rel="stylesheet" />
    </Head>
    
    <div class="min-h-screen bg-cream">
        <Header />
        
        <main class="cart-page">
            <section class="hero-section">
                <div class="hero-content">
                    <h1 class="hero-title">Корзина</h1>
                    <p class="hero-subtitle" v-if="cart.length > 0">В вашей корзине {{ cart.length }} {{ cart.length === 1 ? 'товар' : cart.length < 5 ? 'товара' : 'товаров' }}</p>
                    <p class="hero-subtitle" v-else>Ваша корзина пуста</p>
                </div>
            </section>

            <section class="content-section">
                <div class="container">
                    <div v-if="cart.length === 0" class="empty-cart">
                        <div class="empty-cart-icon">
                            <svg width="120" height="120" viewBox="0 0 65 64" fill="none" xmlns="http://www.w3.org/2000/svg">
                                <path d="M64.3763 22.4948C64.1417 22.224 63.8506 22.0066 63.5229 21.8575C63.1951 21.7084 62.8386 21.6313 62.4778 21.6313H47.4899V11.7627C47.4899 9.79974 46.7004 7.91716 45.295 6.52912C43.8896 5.14109 41.9835 4.3613 39.996 4.3613H25.0081C23.0206 4.3613 21.1145 5.14109 19.7091 6.52912C18.3037 7.91716 17.5142 9.79974 17.5142 11.7627V21.6313H2.52627C2.16417 21.6272 1.80552 21.701 1.47515 21.8474C1.14478 21.9939 0.850603 22.2095 0.612991 22.4794C0.375378 22.7493 0.200016 23.0669 0.0990546 23.4104C-0.00190693 23.7539 -0.0260539 24.1149 0.0282866 24.4685L4.72449 54.4443C4.90515 55.6209 5.51027 56.6933 6.42835 57.4641C7.34643 58.2348 8.5156 58.6519 9.72045 58.6384H55.3336C56.5384 58.6519 57.7076 58.2348 58.6257 57.4641C59.5438 56.6933 60.1489 55.6209 60.3295 54.4443L64.9758 24.4685C65.0258 24.1163 64.9981 23.7575 64.8946 23.4169C64.7912 23.0762 64.6143 22.7616 64.3763 22.4948ZM22.5101 11.7627C22.5101 11.1084 22.7733 10.4809 23.2418 10.0182C23.7102 9.55551 24.3456 9.29558 25.0081 9.29558H39.996C40.6585 9.29558 41.2939 9.55551 41.7623 10.0182C42.2308 10.4809 42.494 11.1084 42.494 11.7627V21.6313H22.5101V11.7627ZM55.3336 53.7041H9.67049L5.4489 26.5656H59.5552L55.3336 53.7041Z" fill="#d7b389"/>
                            </svg>
                        </div>
                        <h2 class="empty-cart-title">Корзина пуста</h2>
                        <p class="empty-cart-text">Добавьте товары из меню, чтобы сделать заказ</p>
                        <Link :href="route('welcome')" class="back-to-menu-btn">
                            Перейти в меню
                        </Link>
                    </div>

                    <div v-else class="cart-content">
                        <div class="cart-items">
                            <div 
                                v-for="(item, index) in cart" 
                                :key="index"
                                class="cart-item"
                            >
                                <div class="cart-item-image">
                                    <img :src="item.image" :alt="item.name" @error="handleImageError" />
                                </div>
                                <div class="cart-item-info">
                                    <h3 class="cart-item-name">{{ item.name }}</h3>
                                    <p class="cart-item-size" v-if="item.sizeLabel">
                                        Размер: {{ item.sizeLabel }}
                                    </p>
                                    <p class="cart-item-price">{{ item.price }}₽</p>
                                </div>
                                <div class="cart-item-controls">
                                    <div class="quantity-controls">
                                        <button 
                                            class="quantity-btn"
                                            @click="updateCartItemQuantity(index, item.quantity - 1)"
                                        >
                                            −
                                        </button>
                                        <span class="quantity-value">{{ item.quantity }}</span>
                                        <button 
                                            class="quantity-btn"
                                            @click="updateCartItemQuantity(index, item.quantity + 1)"
                                        >
                                            +
                                        </button>
                                    </div>
                                    <div class="cart-item-total">
                                        {{ item.price * item.quantity }}₽
                                    </div>
                                    <button 
                                        class="remove-btn"
                                        @click="removeFromCart(index)"
                                        aria-label="Удалить"
                                    >
                                        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                            <path d="M18 6L6 18M6 6L18 18" stroke="#e74c3c" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                                        </svg>
                                    </button>
                                </div>
                            </div>
                        </div>

                        <div class="cart-summary">
                            <div class="summary-card">
                                <h2 class="summary-title">Итого</h2>
                                <div class="summary-row">
                                    <span class="summary-label">Товаров:</span>
                                    <span class="summary-value">{{ cart.reduce((sum, item) => sum + item.quantity, 0) }} шт.</span>
                                </div>
                                <div class="summary-row total-row">
                                    <span class="summary-label">Сумма:</span>
                                    <span class="summary-value total-price">{{ totalPrice }}₽</span>
                                </div>
                                <button class="checkout-btn" @click="handleCheckout">
                                    Оформить заказ
                                </button>
                                <Link :href="route('welcome')" class="continue-shopping">
                                    Продолжить покупки
                                </Link>
                            </div>
                        </div>
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

.cart-page {
    min-height: calc(100vh - 200px);
}

.hero-section {
    background: linear-gradient(135deg, #C85D3E 0%, #B84A3A 100%);
    padding: 80px 20px 60px;
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
    margin: 0 0 16px 0;
    font-weight: bold;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}

.hero-subtitle {
    font-size: 20px;
    color: rgba(255, 255, 255, 0.95);
    margin: 0;
    line-height: 1.6;
}

.content-section {
    padding: 60px 20px;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
}

.empty-cart {
    text-align: center;
    padding: 80px 20px;
}

.empty-cart-icon {
    margin-bottom: 30px;
    opacity: 0.5;
}

.empty-cart-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 32px;
    color: #3D2E28;
    margin: 0 0 16px 0;
}

.empty-cart-text {
    font-size: 18px;
    color: #4A3A2A;
    margin: 0 0 40px 0;
}

.back-to-menu-btn {
    display: inline-block;
    padding: 16px 32px;
    background: linear-gradient(135deg, #B84A3A 0%, #C85D3E 100%);
    color: white;
    border-radius: 12px;
    font-family: "Dela Gothic One", sans-serif;
    font-size: 18px;
    font-weight: bold;
    text-decoration: none;
    transition: all 0.3s ease;
    box-shadow: 0 4px 12px rgba(200, 93, 62, 0.3);
}

.back-to-menu-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(200, 93, 62, 0.4);
}

.cart-content {
    display: grid;
    grid-template-columns: 1fr 400px;
    gap: 40px;
    align-items: start;
}

.cart-items {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.cart-item {
    background: white;
    border-radius: 16px;
    padding: 24px;
    display: flex;
    gap: 20px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
    border: 2px solid #C85D3E;
    transition: all 0.3s ease;
}

.cart-item:hover {
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.12);
    transform: translateY(-2px);
}

.cart-item-image {
    width: 120px;
    height: 120px;
    flex-shrink: 0;
    border-radius: 12px;
    overflow: hidden;
    background: #f5f5f5;
}

.cart-item-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.cart-item-info {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.cart-item-name {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 20px;
    color: #3D2E28;
    margin: 0;
    font-weight: bold;
}

.cart-item-size {
    font-size: 14px;
    color: #4A3A2A;
    margin: 0;
}

.cart-item-price {
    font-size: 16px;
    color: #B84A3A;
    font-weight: 600;
    margin: 0;
}

.cart-item-controls {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 12px;
}

.quantity-controls {
    display: flex;
    align-items: center;
    gap: 12px;
    background: #F5F0E8;
    border-radius: 8px;
    padding: 4px;
    border: 2px solid #C85D3E;
}

.quantity-btn {
    width: 32px;
    height: 32px;
    border: none;
    background: linear-gradient(135deg, #C85D3E 0%, #B84A3A 100%);
    color: white;
    border-radius: 6px;
    font-size: 20px;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: "Dela Gothic One", sans-serif;
}

.quantity-btn:hover {
    background: linear-gradient(135deg, #C85D3E 0%, #B84A3A 100%);
    color: white;
    transform: scale(1.1);
}

.quantity-value {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 18px;
    color: #3D2E28;
    min-width: 30px;
    text-align: center;
    font-weight: bold;
}

.cart-item-total {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 22px;
    color: #B84A3A;
    font-weight: bold;
}

.remove-btn {
    background: transparent;
    border: none;
    cursor: pointer;
    padding: 8px;
    border-radius: 8px;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
}

.remove-btn:hover {
    background: rgba(231, 76, 60, 0.1);
    transform: scale(1.1);
}

.cart-summary {
    position: sticky;
    top: 100px;
}

.summary-card {
    background: white;
    border-radius: 16px;
    padding: 32px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
    border: 2px solid #C85D3E;
}

.summary-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 24px;
    color: #3D2E28;
    margin: 0 0 24px 0;
    font-weight: bold;
}

.summary-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px 0;
    border-bottom: 1px solid rgba(200, 93, 62, 0.3);
}

.summary-row:last-of-type {
    border-bottom: none;
}

.total-row {
    margin-top: 16px;
    padding-top: 20px;
    border-top: 2px solid rgba(200, 93, 62, 0.3);
}

.summary-label {
    font-size: 16px;
    color: #4A3A2A;
}

.summary-value {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 18px;
    color: #3D2E28;
    font-weight: bold;
}

.total-price {
    font-size: 28px;
    color: #B84A3A;
}

.checkout-btn {
    width: 100%;
    padding: 16px;
    margin-top: 24px;
    background: linear-gradient(135deg, #B84A3A 0%, #C85D3E 100%);
    color: white;
    border: none;
    border-radius: 12px;
    font-family: "Dela Gothic One", sans-serif;
    font-size: 18px;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 12px rgba(200, 93, 62, 0.3);
}

.checkout-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(200, 93, 62, 0.4);
}

.continue-shopping {
    display: block;
    text-align: center;
    margin-top: 16px;
    color: #B84A3A;
    text-decoration: none;
    font-size: 16px;
    font-weight: 600;
    transition: all 0.3s ease;
}

.continue-shopping:hover {
    color: #C85D3E;
    text-decoration: underline;
}

@media (max-width: 968px) {
    .cart-content {
        grid-template-columns: 1fr;
        gap: 30px;
    }
    
    .cart-summary {
        position: static;
    }
    
    .hero-section {
        padding: 60px 20px 50px;
    }
    
    .hero-title {
        font-size: 36px;
    }
    
    .hero-subtitle {
        font-size: 18px;
    }
    
    .content-section {
        padding: 50px 20px;
    }
}

@media (max-width: 768px) {
    .hero-section {
        padding: 50px 15px 40px;
    }
    
    .hero-title {
        font-size: 32px;
    }
    
    .hero-subtitle {
        font-size: 16px;
    }
    
    .content-section {
        padding: 40px 15px;
    }
    
    .cart-item {
        padding: 20px;
        gap: 15px;
    }
    
    .cart-item-image {
        width: 100px;
        height: 100px;
    }
    
    .cart-item-name {
        font-size: 18px;
    }
    
    .summary-card {
        padding: 24px;
    }
}

@media (max-width: 640px) {
    .hero-section {
        padding: 40px 15px 30px;
    }
    
    .hero-title {
        font-size: 28px;
    }
    
    .hero-subtitle {
        font-size: 14px;
    }
    
    .content-section {
        padding: 30px 15px;
    }
    
    .cart-item {
        flex-direction: column;
        padding: 16px;
    }
    
    .cart-item-image {
        width: 100%;
        height: 200px;
    }
    
    .cart-item-controls {
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        width: 100%;
    }
    
    .cart-item-total {
        font-size: 20px;
    }
    
    .summary-card {
        padding: 20px;
    }
    
    .summary-title {
        font-size: 20px;
    }
    
    .total-price {
        font-size: 24px;
    }
    
    .checkout-btn {
        padding: 14px;
        font-size: 16px;
    }
    
    .empty-cart {
        padding: 60px 15px;
    }
    
    .empty-cart-title {
        font-size: 28px;
    }
    
    .empty-cart-text {
        font-size: 16px;
    }
    
    .back-to-menu-btn {
        padding: 14px 28px;
        font-size: 16px;
    }
}

@media (max-width: 480px) {
    .hero-title {
        font-size: 24px;
    }
    
    .cart-item-name {
        font-size: 16px;
    }
    
    .cart-item-price {
        font-size: 14px;
    }
    
    .quantity-value {
        font-size: 16px;
    }
    
    .cart-item-total {
        font-size: 18px;
    }
    
    .summary-value {
        font-size: 16px;
    }
    
    .total-price {
        font-size: 22px;
    }
}
</style>

