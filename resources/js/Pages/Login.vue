<script setup>
import { ref, onMounted } from 'vue';
import { Head, Link, useForm, router, usePage } from '@inertiajs/vue3';
import Header from '@/Components/Header.vue';
import Footer from '@/Components/Footer.vue';

const props = defineProps({
    status: {
        type: String,
    },
});

const page = usePage();
const isLogin = ref(true);

// Проверяем query параметр для автоматического переключения на регистрацию
onMounted(() => {
    const urlParams = new URLSearchParams(window.location.search);
    if (urlParams.get('mode') === 'register') {
        isLogin.value = false;
    }
});

const loginForm = useForm({
    email: '',
    password: '',
    remember: false,
});

const registerForm = useForm({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
});

const submitLogin = () => {
    loginForm.post(route('login'), {
        onFinish: () => loginForm.reset('password'),
    });
};

const submitRegister = () => {
    registerForm.post(route('register'), {
        onFinish: () => registerForm.reset('password', 'password_confirmation'),
    });
};

const switchMode = () => {
    isLogin.value = !isLogin.value;
    // Очищаем ошибки при переключении
    loginForm.clearErrors();
    registerForm.clearErrors();
};
</script>

<template>
    <Head title="Вход / Регистрация" />
    
    <div class="min-h-screen bg-cream flex flex-col">
        <Header />
        
        <div class="flex-1 flex items-center justify-center py-12 px-4 sm:px-6 lg:px-8">
            <div class="auth-container">
                <div class="auth-header">
                    <div class="auth-tabs">
                        <button
                            :class="['auth-tab', { active: isLogin }]"
                            @click="switchMode"
                        >
                            Вход
                        </button>
                        <button
                            :class="['auth-tab', { active: !isLogin }]"
                            @click="switchMode"
                        >
                            Регистрация
                        </button>
                    </div>
                </div>

                <div v-if="status" class="status-message">
                    {{ status }}
                </div>

                <!-- Форма входа -->
                <form v-if="isLogin" @submit.prevent="submitLogin" class="auth-form">
                    <div class="form-group">
                        <label for="login-email" class="form-label">Email</label>
                        <input
                            id="login-email"
                            type="email"
                            class="form-input"
                            v-model="loginForm.email"
                            required
                            autofocus
                            autocomplete="username"
                            placeholder="Введите ваш email"
                        />
                        <div v-if="loginForm.errors.email" class="error-message">
                            {{ loginForm.errors.email }}
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="login-password" class="form-label">Пароль</label>
                        <input
                            id="login-password"
                            type="password"
                            class="form-input"
                            v-model="loginForm.password"
                            required
                            autocomplete="current-password"
                            placeholder="Введите пароль"
                        />
                        <div v-if="loginForm.errors.password" class="error-message">
                            {{ loginForm.errors.password }}
                        </div>
                    </div>

                    <div class="form-group checkbox-group">
                        <label class="checkbox-label">
                            <input
                                type="checkbox"
                                v-model="loginForm.remember"
                                class="checkbox-input"
                            />
                            <span class="checkbox-text">Запомнить меня</span>
                        </label>
                    </div>

                    <button
                        type="submit"
                        class="submit-btn"
                        :class="{ 'opacity-50': loginForm.processing }"
                        :disabled="loginForm.processing"
                    >
                        {{ loginForm.processing ? 'Вход...' : 'Войти' }}
                    </button>
                </form>

                <!-- Форма регистрации -->
                <form v-else @submit.prevent="submitRegister" class="auth-form">
                    <div class="form-group">
                        <label for="register-name" class="form-label">Имя</label>
                        <input
                            id="register-name"
                            type="text"
                            class="form-input"
                            v-model="registerForm.name"
                            required
                            autofocus
                            autocomplete="name"
                            placeholder="Введите ваше имя"
                        />
                        <div v-if="registerForm.errors.name" class="error-message">
                            {{ registerForm.errors.name }}
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="register-email" class="form-label">Email</label>
                        <input
                            id="register-email"
                            type="email"
                            class="form-input"
                            v-model="registerForm.email"
                            required
                            autocomplete="username"
                            placeholder="Введите ваш email"
                        />
                        <div v-if="registerForm.errors.email" class="error-message">
                            {{ registerForm.errors.email }}
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="register-password" class="form-label">Пароль</label>
                        <input
                            id="register-password"
                            type="password"
                            class="form-input"
                            v-model="registerForm.password"
                            required
                            autocomplete="new-password"
                            placeholder="Введите пароль"
                        />
                        <div v-if="registerForm.errors.password" class="error-message">
                            {{ registerForm.errors.password }}
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="register-password-confirmation" class="form-label">Подтвердите пароль</label>
                        <input
                            id="register-password-confirmation"
                            type="password"
                            class="form-input"
                            v-model="registerForm.password_confirmation"
                            required
                            autocomplete="new-password"
                            placeholder="Повторите пароль"
                        />
                        <div v-if="registerForm.errors.password_confirmation" class="error-message">
                            {{ registerForm.errors.password_confirmation }}
                        </div>
                    </div>

                    <button
                        type="submit"
                        class="submit-btn"
                        :class="{ 'opacity-50': registerForm.processing }"
                        :disabled="registerForm.processing"
                    >
                        {{ registerForm.processing ? 'Регистрация...' : 'Зарегистрироваться' }}
                    </button>
                </form>
            </div>
        </div>
        
        <Footer />
    </div>
</template>

<style scoped>
.bg-cream {
    background-color: #F8F5F0;
}

.auth-container {
    width: 100%;
    max-width: 480px;
    background: white;
    border-radius: 24px;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
    overflow: hidden;
    border: 2px solid rgba(232, 221, 208, 0.6);
}

.auth-header {
    background: linear-gradient(135deg, #C85D3E 0%, #B84A3A 100%);
    padding: 24px;
}

.auth-tabs {
    display: flex;
    gap: 8px;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 16px;
    padding: 4px;
}

.auth-tab {
    flex: 1;
    padding: 12px 24px;
    background: transparent;
    border: none;
    border-radius: 12px;
    color: rgba(255, 255, 255, 0.7);
    font-family: "Dela Gothic One", sans-serif;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s ease;
}

.auth-tab:hover {
    color: white;
    background: rgba(255, 255, 255, 0.1);
}

.auth-tab.active {
    background: white;
    color: #B84A3A;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}

.status-message {
    margin: 20px 30px 0;
    padding: 12px 16px;
    background: #d4edda;
    border: 1px solid #c3e6cb;
    border-radius: 12px;
    color: #155724;
    font-size: 14px;
    text-align: center;
}

.auth-form {
    padding: 30px;
}

.form-group {
    margin-bottom: 20px;
}

.form-label {
    display: block;
    font-family: "Dela Gothic One", sans-serif;
    font-size: 14px;
    color: #3D2E28;
    margin-bottom: 8px;
    font-weight: bold;
}

.form-input {
    width: 100%;
    padding: 14px 16px;
    border: 2px solid rgba(232, 221, 208, 0.6);
    border-radius: 12px;
    font-size: 16px;
    font-family: sans-serif;
    color: #3D2E28;
    background: #F5F0E8;
    transition: all 0.3s ease;
    box-sizing: border-box;
}

.form-input:focus {
    outline: none;
    border-color: #C85D3E;
    background: white;
    box-shadow: 0 0 0 3px rgba(200, 93, 62, 0.1);
}

.form-input::placeholder {
    color: #9ca3af;
}

.error-message {
    margin-top: 6px;
    font-size: 13px;
    color: #B84A3A;
    font-weight: 500;
}

.checkbox-group {
    margin-bottom: 24px;
}

.checkbox-label {
    display: flex;
    align-items: center;
    cursor: pointer;
}

.checkbox-input {
    width: 18px;
    height: 18px;
    margin-right: 10px;
    cursor: pointer;
    accent-color: #C85D3E;
}

.checkbox-text {
    font-size: 14px;
    color: #6B5A4A;
    user-select: none;
}

.submit-btn {
    width: 100%;
    padding: 16px 24px;
    background: linear-gradient(135deg, #C85D3E 0%, #B84A3A 100%);
    color: white;
    border: none;
    border-radius: 14px;
    font-weight: bold;
    font-size: 18px;
    font-family: "Dela Gothic One", sans-serif;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 12px rgba(200, 93, 62, 0.25);
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

.submit-btn:hover:not(:disabled) {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(200, 93, 62, 0.4);
}

.submit-btn:active:not(:disabled) {
    transform: translateY(0);
}

.submit-btn:disabled {
    cursor: not-allowed;
}

@media (max-width: 640px) {
    .auth-container {
        max-width: 100%;
        margin: 0 15px;
        border-radius: 20px;
    }
    
    .auth-header {
        padding: 20px;
    }
    
    .auth-tab {
        padding: 10px 16px;
        font-size: 14px;
    }
    
    .auth-form {
        padding: 24px 20px;
    }
    
    .form-group {
        margin-bottom: 18px;
    }
    
    .form-input {
        padding: 12px 14px;
        font-size: 15px;
    }
    
    .submit-btn {
        padding: 14px 20px;
        font-size: 16px;
    }
}

@media (max-width: 480px) {
    .auth-container {
        margin: 0 10px;
        border-radius: 16px;
    }
    
    .auth-header {
        padding: 16px;
    }
    
    .auth-tabs {
        padding: 3px;
    }
    
    .auth-tab {
        padding: 8px 12px;
        font-size: 13px;
    }
    
    .auth-form {
        padding: 20px 16px;
    }
    
    .form-label {
        font-size: 13px;
    }
    
    .form-input {
        padding: 10px 12px;
        font-size: 14px;
    }
    
    .submit-btn {
        padding: 12px 16px;
        font-size: 15px;
    }
}
</style>

