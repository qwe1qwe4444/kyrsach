<script setup>
import { ref } from 'vue';
import { Head, useForm, usePage, router } from '@inertiajs/vue3';
import Header from '@/Components/Header.vue';
import Footer from '@/Components/Footer.vue';

const props = defineProps({
    status: {
        type: String,
    },
});

const page = usePage();
const user = page.props.auth.user;

const activeTab = ref('orders'); // orders, info, settings

// Форма информации профиля
const profileForm = useForm({
    name: user.name || '',
    email: user.email || '',
    phone: user.phone || '',
    address: user.address || '',
    birth_date: user.birth_date || '',
});

// Форма смены пароля
const passwordForm = useForm({
    current_password: '',
    password: '',
    password_confirmation: '',
});

// Форма удаления аккаунта
const deleteForm = useForm({
    password: '',
});

const updateProfile = () => {
    profileForm.patch(route('profile.update'), {
        preserveScroll: true,
        onSuccess: () => {
            // Успешно обновлено
        },
    });
};

const updatePassword = () => {
    passwordForm.put(route('profile.password.update'), {
        preserveScroll: true,
        onSuccess: () => {
            passwordForm.reset();
        },
        onError: () => {
            if (passwordForm.errors.password) {
                passwordForm.reset('password', 'password_confirmation');
            }
            if (passwordForm.errors.current_password) {
                passwordForm.reset('current_password');
            }
        },
    });
};

const deleteAccount = () => {
    if (confirm('Вы уверены, что хотите удалить свой аккаунт? Это действие необратимо.')) {
        deleteForm.delete(route('profile.destroy'), {
            preserveScroll: true,
            onSuccess: () => {
                router.visit('/');
            },
        });
    }
};

// История заказов (пример данных, можно будет подключить к БД)
const orders = ref([
    {
        id: 1,
        date: '2024-01-15',
        total: 2450,
        status: 'Доставлен',
        items: [
            { name: 'Пицца "4 Сыра"', size: '35 см', quantity: 1, price: 1790 },
            { name: 'Кола', quantity: 2, price: 150 },
        ],
    },
    {
        id: 2,
        date: '2024-01-10',
        total: 1890,
        status: 'Доставлен',
        items: [
            { name: 'Мясная', size: '35 см', quantity: 1, price: 1890 },
        ],
    },
    {
        id: 3,
        date: '2024-01-05',
        total: 3200,
        status: 'В пути',
        items: [
            { name: 'Пепперони', size: '45 см', quantity: 1, price: 2050 },
            { name: 'Картофель фри', quantity: 1, price: 250 },
            { name: 'Куриные крылышки', quantity: 1, price: 390 },
            { name: 'Кола', quantity: 2, price: 150 },
        ],
    },
]);

const repeatOrder = (order) => {
    // Добавляем товары из заказа в корзину
    const cart = JSON.parse(localStorage.getItem('cart') || '[]');
    
    order.items.forEach(item => {
        const existingItem = cart.find(
            i => i.name === item.name && i.size === (item.size || 'single')
        );
        
        if (existingItem) {
            existingItem.quantity += item.quantity;
        } else {
            cart.push({
                productId: Date.now() + Math.random(),
                name: item.name,
                size: item.size || 'single',
                sizeLabel: item.size || '',
                price: item.price,
                quantity: item.quantity,
                hasSizes: !!item.size,
            });
        }
    });
    
    localStorage.setItem('cart', JSON.stringify(cart));
    window.dispatchEvent(new Event('cartUpdated'));
    router.visit(route('cart'));
};
</script>

<template>
    <Head title="Профиль" />
    
    <div class="min-h-screen bg-cream flex flex-col">
        <Header />
        
        <div class="flex-1 container mx-auto px-4 py-8 max-w-6xl">
            <div class="profile-container">
                <h1 class="profile-title">Личный кабинет</h1>
                
                <!-- Вкладки -->
                <div class="tabs">
                    <button
                        :class="['tab', { active: activeTab === 'orders' }]"
                        @click="activeTab = 'orders'"
                    >
                        История заказов
                    </button>
                    <button
                        :class="['tab', { active: activeTab === 'info' }]"
                        @click="activeTab = 'info'"
                    >
                        Информация
                    </button>
                    <button
                        :class="['tab', { active: activeTab === 'settings' }]"
                        @click="activeTab = 'settings'"
                    >
                        Настройки
                    </button>
                </div>
                
                <!-- Контент вкладок -->
                <div class="tab-content">
                    <!-- История заказов -->
                    <div v-if="activeTab === 'orders'" class="tab-panel">
                        <h2 class="section-title">История заказов</h2>
                        
                        <div v-if="orders.length === 0" class="empty-state">
                            <p>У вас пока нет заказов</p>
                        </div>
                        
                        <div v-else class="orders-list">
                            <div v-for="order in orders" :key="order.id" class="order-card">
                                <div class="order-header">
                                    <div class="order-info">
                                        <span class="order-number">Заказ №{{ order.id }}</span>
                                        <span class="order-date">{{ new Date(order.date).toLocaleDateString('ru-RU') }}</span>
                                    </div>
                                    <div class="order-status" :class="`status-${order.status.toLowerCase().replace(' ', '-')}`">
                                        {{ order.status }}
                                    </div>
                                </div>
                                
                                <div class="order-items">
                                    <div v-for="(item, index) in order.items" :key="index" class="order-item">
                                        <span class="item-name">{{ item.name }}{{ item.size ? ` (${item.size})` : '' }}</span>
                                        <span class="item-quantity">×{{ item.quantity }}</span>
                                        <span class="item-price">{{ item.price }}₽</span>
                                    </div>
                                </div>
                                
                                <div class="order-footer">
                                    <div class="order-total">
                                        <span>Итого:</span>
                                        <span class="total-price">{{ order.total }}₽</span>
                                    </div>
                                    <button class="repeat-btn" @click="repeatOrder(order)">
                                        Повторить заказ
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Информация -->
                    <div v-if="activeTab === 'info'" class="tab-panel">
                        <h2 class="section-title">Личная информация</h2>
                        
                        <form @submit.prevent="updateProfile" class="profile-form">
                            <div class="form-group">
                                <label for="name" class="form-label">ФИО</label>
                                <input
                                    id="name"
                                    type="text"
                                    class="form-input"
                                    v-model="profileForm.name"
                                    required
                                    placeholder="Введите ваше ФИО"
                                />
                                <div v-if="profileForm.errors.name" class="error-message">
                                    {{ profileForm.errors.name }}
                                </div>
                            </div>
                            
                            <div class="form-group">
                                <label for="email" class="form-label">Email</label>
                                <input
                                    id="email"
                                    type="email"
                                    class="form-input"
                                    v-model="profileForm.email"
                                    required
                                    placeholder="Введите ваш email"
                                />
                                <div v-if="profileForm.errors.email" class="error-message">
                                    {{ profileForm.errors.email }}
                                </div>
                            </div>
                            
                            <div class="form-group">
                                <label for="phone" class="form-label">Телефон</label>
                                <input
                                    id="phone"
                                    type="tel"
                                    class="form-input"
                                    v-model="profileForm.phone"
                                    placeholder="+7 (999) 123-45-67"
                                />
                                <div v-if="profileForm.errors.phone" class="error-message">
                                    {{ profileForm.errors.phone }}
                                </div>
                            </div>
                            
                            <div class="form-group">
                                <label for="address" class="form-label">Адрес доставки</label>
                                <textarea
                                    id="address"
                                    class="form-input form-textarea"
                                    v-model="profileForm.address"
                                    rows="3"
                                    placeholder="Введите адрес доставки"
                                ></textarea>
                                <div v-if="profileForm.errors.address" class="error-message">
                                    {{ profileForm.errors.address }}
                                </div>
                            </div>
                            
                            <div class="form-group">
                                <label for="birth_date" class="form-label">Дата рождения</label>
                                <input
                                    id="birth_date"
                                    type="date"
                                    class="form-input"
                                    v-model="profileForm.birth_date"
                                />
                                <div v-if="profileForm.errors.birth_date" class="error-message">
                                    {{ profileForm.errors.birth_date }}
                                </div>
                            </div>
                            
                            <button
                                type="submit"
                                class="submit-btn"
                                :class="{ 'opacity-50': profileForm.processing }"
                                :disabled="profileForm.processing"
                            >
                                {{ profileForm.processing ? 'Сохранение...' : 'Сохранить изменения' }}
                            </button>
                            
                            <Transition
                                enter-active-class="transition ease-in-out"
                                enter-from-class="opacity-0"
                                leave-active-class="transition ease-in-out"
                                leave-to-class="opacity-0"
                            >
                                <p v-if="profileForm.recentlySuccessful" class="success-message">
                                    Изменения сохранены
                                </p>
                            </Transition>
                        </form>
                    </div>
                    
                    <!-- Настройки -->
                    <div v-if="activeTab === 'settings'" class="tab-panel">
                        <h2 class="section-title">Настройки</h2>
                        
                        <!-- Смена пароля -->
                        <div class="settings-section">
                            <h3 class="settings-title">Смена пароля</h3>
                            <form @submit.prevent="updatePassword" class="profile-form">
                                <div class="form-group">
                                    <label for="current_password" class="form-label">Текущий пароль</label>
                                    <input
                                        id="current_password"
                                        type="password"
                                        class="form-input"
                                        v-model="passwordForm.current_password"
                                        required
                                        placeholder="Введите текущий пароль"
                                    />
                                    <div v-if="passwordForm.errors.current_password" class="error-message">
                                        {{ passwordForm.errors.current_password }}
                                    </div>
                                </div>
                                
                                <div class="form-group">
                                    <label for="password" class="form-label">Новый пароль</label>
                                    <input
                                        id="password"
                                        type="password"
                                        class="form-input"
                                        v-model="passwordForm.password"
                                        required
                                        placeholder="Введите новый пароль"
                                    />
                                    <div v-if="passwordForm.errors.password" class="error-message">
                                        {{ passwordForm.errors.password }}
                                    </div>
                                </div>
                                
                                <div class="form-group">
                                    <label for="password_confirmation" class="form-label">Подтвердите пароль</label>
                                    <input
                                        id="password_confirmation"
                                        type="password"
                                        class="form-input"
                                        v-model="passwordForm.password_confirmation"
                                        required
                                        placeholder="Повторите новый пароль"
                                    />
                                    <div v-if="passwordForm.errors.password_confirmation" class="error-message">
                                        {{ passwordForm.errors.password_confirmation }}
                                    </div>
                                </div>
                                
                                <button
                                    type="submit"
                                    class="submit-btn"
                                    :class="{ 'opacity-50': passwordForm.processing }"
                                    :disabled="passwordForm.processing"
                                >
                                    {{ passwordForm.processing ? 'Сохранение...' : 'Изменить пароль' }}
                                </button>
                                
                                <Transition
                                    enter-active-class="transition ease-in-out"
                                    enter-from-class="opacity-0"
                                    leave-active-class="transition ease-in-out"
                                    leave-to-class="opacity-0"
                                >
                                    <p v-if="passwordForm.recentlySuccessful" class="success-message">
                                        Пароль успешно изменен
                                    </p>
                                </Transition>
                            </form>
                        </div>
                        
                        <!-- Удаление аккаунта -->
                        <div class="settings-section danger-section">
                            <h3 class="settings-title danger-title">Удаление аккаунта</h3>
                            <p class="danger-description">
                                После удаления аккаунта все ваши данные будут безвозвратно удалены. Это действие необратимо.
                            </p>
                            <form @submit.prevent="deleteAccount" class="profile-form">
                                <div class="form-group">
                                    <label for="delete_password" class="form-label">Подтвердите пароль</label>
                                    <input
                                        id="delete_password"
                                        type="password"
                                        class="form-input"
                                        v-model="deleteForm.password"
                                        required
                                        placeholder="Введите пароль для подтверждения"
                                    />
                                    <div v-if="deleteForm.errors.password" class="error-message">
                                        {{ deleteForm.errors.password }}
                                    </div>
                                </div>
                                
                                <button
                                    type="submit"
                                    class="danger-btn"
                                    :class="{ 'opacity-50': deleteForm.processing }"
                                    :disabled="deleteForm.processing"
                                >
                                    {{ deleteForm.processing ? 'Удаление...' : 'Удалить аккаунт' }}
                                </button>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <Footer />
    </div>
</template>

<style scoped>
.bg-cream {
    background-color: #F8F5F0;
}

.profile-container {
    background: white;
    border-radius: 24px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
    overflow: hidden;
    border: 2px solid rgba(232, 221, 208, 0.6);
}

.profile-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 32px;
    color: #3D2E28;
    padding: 30px 30px 20px;
    margin: 0;
    border-bottom: 2px solid rgba(232, 221, 208, 0.5);
}

.tabs {
    display: flex;
    background: #F5F0E8;
    border-bottom: 2px solid rgba(232, 221, 208, 0.5);
    padding: 0 30px;
    gap: 0;
}

.tab {
    padding: 16px 24px;
    background: transparent;
    border: none;
    border-bottom: 3px solid transparent;
    font-family: "Dela Gothic One", sans-serif;
    font-size: 16px;
    color: #6B5A4A;
    cursor: pointer;
    transition: all 0.3s ease;
    position: relative;
    top: 2px;
}

.tab:hover {
    color: #C85D3E;
    background: rgba(200, 93, 62, 0.05);
}

.tab.active {
    color: #B84A3A;
    border-bottom-color: #B84A3A;
    background: white;
}

.tab-content {
    padding: 30px;
}

.tab-panel {
    animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(10px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.section-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 24px;
    color: #3D2E28;
    margin: 0 0 24px 0;
}

.empty-state {
    text-align: center;
    padding: 60px 20px;
    color: #6B5A4A;
}

.empty-state p {
    font-size: 18px;
    font-family: "Dela Gothic One", sans-serif;
}

/* История заказов */
.orders-list {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.order-card {
    background: #F5F0E8;
    border: 2px solid rgba(232, 221, 208, 0.6);
    border-radius: 16px;
    padding: 20px;
    transition: all 0.3s ease;
}

.order-card:hover {
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    border-color: #C85D3E;
}

.order-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 16px;
    padding-bottom: 12px;
    border-bottom: 2px solid rgba(232, 221, 208, 0.5);
}

.order-info {
    display: flex;
    flex-direction: column;
    gap: 4px;
}

.order-number {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 18px;
    color: #3D2E28;
}

.order-date {
    font-size: 14px;
    color: #6B5A4A;
    font-family: "Dela Gothic One", sans-serif;
}

.order-status {
    padding: 6px 16px;
    border-radius: 20px;
    font-size: 14px;
    font-weight: bold;
    font-family: "Dela Gothic One", sans-serif;
}

.status-доставлен {
    background: #d4edda;
    color: #155724;
}

.status-в-пути {
    background: #fff3cd;
    color: #856404;
}

.status-готовится {
    background: #cfe2ff;
    color: #084298;
}

.order-items {
    display: flex;
    flex-direction: column;
    gap: 8px;
    margin-bottom: 16px;
}

.order-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 8px 0;
}

.item-name {
    flex: 1;
    color: #3D2E28;
    font-weight: 500;
    font-family: "Dela Gothic One", sans-serif;
}

.item-quantity {
    color: #6B5A4A;
    margin: 0 12px;
    font-family: "Dela Gothic One", sans-serif;
}

.item-price {
    color: #B84A3A;
    font-weight: bold;
    font-family: "Dela Gothic One", sans-serif;
}

.order-footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 16px;
    border-top: 2px solid rgba(232, 221, 208, 0.5);
}

.order-total {
    display: flex;
    gap: 12px;
    font-family: "Dela Gothic One", sans-serif;
    font-size: 20px;
    color: #3D2E28;
}

.total-price {
    color: #B84A3A;
}

.repeat-btn {
    padding: 10px 20px;
    background: linear-gradient(135deg, #C85D3E 0%, #B84A3A 100%);
    color: white;
    border: none;
    border-radius: 12px;
    font-family: "Dela Gothic One", sans-serif;
    font-size: 14px;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 2px 8px rgba(200, 93, 62, 0.25);
}

.repeat-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(230, 57, 70, 0.4);
}

/* Формы */
.profile-form {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.form-group {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.form-label {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 14px;
    color: #3D2E28;
    font-weight: bold;
}

.form-input {
    padding: 12px 16px;
    border: 2px solid rgba(232, 221, 208, 0.6);
    border-radius: 12px;
    font-size: 16px;
    font-family: sans-serif;
    color: #3D2E28;
    background: #F5F0E8;
    transition: all 0.3s ease;
}

.form-input:focus {
    outline: none;
    border-color: #C85D3E;
    background: white;
    box-shadow: 0 0 0 3px rgba(255, 107, 53, 0.1);
}

.form-textarea {
    resize: vertical;
    min-height: 80px;
}

.error-message {
    font-size: 13px;
    color: #B84A3A;
    font-weight: 500;
    font-family: "Dela Gothic One", sans-serif;
}

.success-message {
    font-size: 14px;
    color: #155724;
    background: #d4edda;
    padding: 12px 16px;
    border-radius: 12px;
    border: 1px solid #c3e6cb;
    font-family: "Dela Gothic One", sans-serif;
}

.submit-btn {
    padding: 14px 24px;
    background: linear-gradient(135deg, #C85D3E 0%, #B84A3A 100%);
    color: white;
    border: none;
    border-radius: 14px;
    font-weight: bold;
    font-size: 16px;
    font-family: "Dela Gothic One", sans-serif;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 12px rgba(200, 93, 62, 0.25);
    text-transform: uppercase;
    letter-spacing: 0.5px;
    align-self: flex-start;
}

.submit-btn:hover:not(:disabled) {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(200, 93, 62, 0.4);
}

.submit-btn:disabled {
    cursor: not-allowed;
}

/* Настройки */
.settings-section {
    margin-bottom: 40px;
    padding-bottom: 40px;
    border-bottom: 2px solid rgba(232, 221, 208, 0.5);
}

.settings-section:last-child {
    border-bottom: none;
    margin-bottom: 0;
    padding-bottom: 0;
}

.settings-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 20px;
    color: #3D2E28;
    margin: 0 0 16px 0;
}

.danger-section {
    background: #fff5f5;
    padding: 24px;
    border-radius: 16px;
    border: 2px solid #fecaca;
}

.danger-title {
    color: #B84A3A;
}

.danger-description {
    color: #6B5A4A;
    margin-bottom: 20px;
    line-height: 1.6;
    font-family: "Dela Gothic One", sans-serif;
}

.danger-btn {
    padding: 14px 24px;
    background: #B84A3A;
    color: white;
    border: none;
    border-radius: 14px;
    font-weight: bold;
    font-size: 16px;
    font-family: "Dela Gothic One", sans-serif;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 12px rgba(200, 93, 62, 0.25);
    text-transform: uppercase;
    letter-spacing: 0.5px;
    align-self: flex-start;
}

.danger-btn:hover:not(:disabled) {
    background: #A63D2E;
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(200, 93, 62, 0.4);
}

.danger-btn:disabled {
    cursor: not-allowed;
}

@media (max-width: 768px) {
    .profile-title {
        font-size: 24px;
        padding: 20px 20px 16px;
    }
    
    .tabs {
        padding: 0 20px;
        overflow-x: auto;
    }
    
    .tab {
        padding: 12px 16px;
        font-size: 14px;
        white-space: nowrap;
    }
    
    .tab-content {
        padding: 20px;
    }
    
    .section-title {
        font-size: 20px;
    }
    
    .order-header {
        flex-direction: column;
        align-items: flex-start;
        gap: 12px;
    }
    
    .order-footer {
        flex-direction: column;
        gap: 16px;
        align-items: stretch;
    }
    
    .repeat-btn {
        width: 100%;
    }
}

@media (max-width: 480px) {
    .profile-title {
        font-size: 20px;
        padding: 16px 16px 12px;
    }
    
    .tab {
        padding: 10px 12px;
        font-size: 13px;
    }
    
    .tab-content {
        padding: 16px;
    }
    
    .order-card {
        padding: 16px;
    }
    
    .order-number {
        font-size: 16px;
    }
}
</style>

