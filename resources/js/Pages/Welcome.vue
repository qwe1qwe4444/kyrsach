<script setup>
import { Head, Link } from '@inertiajs/vue3';
import { ref, provide } from 'vue';
import Header from '@/Components/Header.vue';
import Hero from '@/Components/Hero.vue';
import Categories from '@/Components/Categories.vue';
import Products from '@/Components/Products.vue';
import Footer from '@/Components/Footer.vue';

defineProps({
    canLogin: {
        type: Boolean,
    },
    canRegister: {
        type: Boolean,
    },
});

// Общее состояние для категорий и поиска
const activeCategory = ref(2); // По умолчанию "Пиццы"
const searchQuery = ref('');

const setActiveCategory = (categoryId) => {
    activeCategory.value = categoryId;
    searchQuery.value = ''; // Очищаем поиск при смене категории
};

const setSearchQuery = (query) => {
    searchQuery.value = query;
};

// Состояние корзины
const cart = ref([]);

const addToCart = (item) => {
    const existingItem = cart.value.find(
        i => i.productId === item.productId && i.size === item.size
    );
    if (existingItem) {
        existingItem.quantity += 1;
    } else {
        cart.value.push({ ...item, quantity: 1 });
    }
    // Сохраняем в localStorage
    localStorage.setItem('cart', JSON.stringify(cart.value));
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

// Загружаем корзину из localStorage при инициализации
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

loadCart();

// Предоставляем состояние дочерним компонентам
provide('activeCategory', activeCategory);
provide('setActiveCategory', setActiveCategory);
provide('searchQuery', searchQuery);
provide('setSearchQuery', setSearchQuery);
provide('cart', cart);
provide('addToCart', addToCart);
provide('removeFromCart', removeFromCart);
provide('updateCartItemQuantity', updateCartItemQuantity);
provide('clearCart', clearCart);
</script>

<template>
    <Head title="Пицца от Дениса - Главная">
        <link rel="preconnect" href="https://fonts.googleapis.com" />
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
        <link href="https://fonts.googleapis.com/css2?family=Dela+Gothic+One&display=swap" rel="stylesheet" />
    </Head>
    
    <div class="min-h-screen bg-cream">
        <Header />
        <Hero />
        <Categories />
        <Products />
        <Footer />
        
        <!-- Auth Links (optional, can be removed if not needed) -->
        <div v-if="canLogin" class="auth-links">
            <Link
                v-if="$page.props.auth?.user"
                :href="route('dashboard')"
                class="auth-btn auth-btn-primary"
            >
                Личный кабинет
            </Link>
            <template v-else>
                <Link
                    :href="route('login')"
                    class="auth-btn auth-btn-primary"
                >
                    Войти
                </Link>
                <Link
                    v-if="canRegister"
                    :href="route('register')"
                    class="auth-btn auth-btn-secondary"
                >
                    Регистрация
                </Link>
            </template>
        </div>
    </div>
</template>

<style scoped>
.bg-cream {
    background-color: #fffaf4;
}

.auth-links {
    position: fixed;
    top: 20px;
    right: 20px;
    z-index: 50;
    display: flex;
    gap: 12px;
}

.auth-btn {
    padding: 10px 20px;
    border-radius: 12px;
    font-weight: 600;
    font-size: 14px;
    font-family: "Dela Gothic One", sans-serif;
    transition: all 0.3s ease;
    text-decoration: none;
    display: inline-block;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}

.auth-btn-primary {
    background: #d7b389;
    color: #3b2b1f;
}

.auth-btn-primary:hover {
    background: #c49a6c;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.auth-btn-secondary {
    background: #99582A;
    color: #fff;
}

.auth-btn-secondary:hover {
    background: #8a4d25;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(153, 88, 42, 0.3);
}

@media (max-width: 768px) {
    .auth-links {
        top: 10px;
        right: 10px;
        flex-direction: column;
        gap: 8px;
    }
    
    .auth-btn {
        padding: 8px 16px;
        font-size: 12px;
    }
}
</style>
