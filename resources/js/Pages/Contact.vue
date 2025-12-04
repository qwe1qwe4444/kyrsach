<script setup>
import { Head, Link } from '@inertiajs/vue3';
import { ref } from 'vue';
import Header from '@/Components/Header.vue';
import Footer from '@/Components/Footer.vue';

const formData = ref({
    name: '',
    email: '',
    phone: '',
    message: ''
});

const handleSubmit = () => {
    // Здесь будет обработка отправки формы
    alert('Спасибо за ваше сообщение! Мы свяжемся с вами в ближайшее время.');
    formData.value = {
        name: '',
        email: '',
        phone: '',
        message: ''
    };
};
</script>

<template>
    <Head title="Связаться с нами - Пицца от Дениса">
        <link rel="preconnect" href="https://fonts.googleapis.com" />
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
        <link href="https://fonts.googleapis.com/css2?family=Dela+Gothic+One&display=swap" rel="stylesheet" />
    </Head>
    
    <div class="min-h-screen bg-cream">
        <Header />
        
        <main class="contact-page">
            <section class="hero-section">
                <div class="hero-content">
                    <h1 class="hero-title">Связаться с нами</h1>
                    <p class="hero-subtitle">Мы всегда рады услышать ваше мнение и ответить на вопросы</p>
                </div>
            </section>

            <section class="content-section">
                <div class="container">
                    <div class="contact-grid">
                        <div class="contact-info">
                            <h2 class="section-title">Наши контакты</h2>
                            
                            <div class="contact-item">
                                <div class="contact-icon">
                                    <svg width="32" height="32" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                        <path d="M3 5C3 3.89543 3.89543 3 5 3H8.27924C8.70967 3 9.09181 3.27543 9.22792 3.68377L10.7257 8.17721C10.8831 8.64932 10.6694 9.16531 10.2243 9.38787L7.96701 10.5165C9.06925 12.9612 11.0388 14.9308 13.4835 16.033L14.6121 13.7757C14.8347 13.3306 15.3507 13.1169 15.8228 13.2743L20.3162 14.7721C20.7246 14.9082 21 15.2903 21 15.7208V19C21 20.1046 20.1046 21 19 21H18C9.71573 21 3 14.2843 3 6V5Z" fill="#99582A"/>
                                    </svg>
                                </div>
                                <div class="contact-details">
                                    <h3 class="contact-label">Телефон</h3>
                                    <p class="contact-value">+7 (999) 123-45-67</p>
                                    <p class="contact-value">+7 (999) 123-45-68</p>
                                </div>
                            </div>

                            <div class="contact-item">
                                <div class="contact-icon">
                                    <svg width="32" height="32" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                        <path d="M3 8L10.89 13.26C11.2187 13.4793 11.6049 13.5963 12 13.5963C12.3951 13.5963 12.7813 13.4793 13.11 13.26L21 8M5 19H19C19.5304 19 20.0391 18.7893 20.4142 18.4142C20.7893 18.0391 21 17.5304 21 17V7C21 6.46957 20.7893 5.96086 20.4142 5.58579C20.0391 5.21071 19.5304 5 19 5H5C4.46957 5 3.96086 5.21071 3.58579 5.58579C3.21071 5.96086 3 6.46957 3 7V17C3 17.5304 3.21071 18.0391 3.58579 18.4142C3.96086 18.7893 4.46957 19 5 19Z" stroke="#99582A" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                                    </svg>
                                </div>
                                <div class="contact-details">
                                    <h3 class="contact-label">Email</h3>
                                    <p class="contact-value">info@pizza-denis.ru</p>
                                    <p class="contact-value">orders@pizza-denis.ru</p>
                                </div>
                            </div>

                            <div class="contact-item">
                                <div class="contact-icon">
                                    <svg width="32" height="32" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                        <path d="M21 10C21 17 12 23 12 23C12 23 3 17 3 10C3 7.61305 3.94821 5.32387 5.63604 3.63604C7.32387 1.94821 9.61305 1 12 1C14.3869 1 16.6761 1.94821 18.364 3.63604C20.0518 5.32387 21 7.61305 21 10Z" stroke="#99582A" stroke-width="2"/>
                                        <path d="M12 13C13.6569 13 15 11.6569 15 10C15 8.34315 13.6569 7 12 7C10.3431 7 9 8.34315 9 10C9 11.6569 10.3431 13 12 13Z" stroke="#99582A" stroke-width="2"/>
                                    </svg>
                                </div>
                                <div class="contact-details">
                                    <h3 class="contact-label">Адрес</h3>
                                    <p class="contact-value">г. Москва, ул. Пиццерийная, д. 1</p>
                                    <p class="contact-value">Время работы: 10:00 - 23:00</p>
                                </div>
                            </div>

                            <div class="social-section">
                                <h3 class="social-title">Мы в соцсетях</h3>
                                <div class="social-links">
                                    <a href="#" class="social-link" aria-label="ВКонтакте">
                                        <svg width="32" height="32" viewBox="0 0 24 24" fill="currentColor">
                                            <path d="M12.785 16.241s.336-.039.508-.23c.099-.14.097-.4.097-.4l-.006-1.28c0-.24.006-3.24.006-3.24s.003-.2.07-.3c.068-.1.19-.13.19-.13l2.8-.02s.15-.01.22.07c.07.08.05.23.05.23l-1.12 5.25s-.07.18-.06.25c.01.07.08.12.14.12l1.5-.02s.9.05.99.08c.1.03.16.12.12.24l-.5 1.5s-.04.1-.12.15c-.08.05-.19.04-.19.04l-2.1-.02s-.15.01-.23-.05c-.08-.06-.06-.18-.06-.18l.5-2.5s.03-.15-.01-.2c-.04-.05-.12-.05-.19-.05l-1.6.02s-.2.01-.28.08c-.08.07-.05.2-.05.2l.5 2.4s.02.12-.02.18c-.04.06-.12.06-.19.06l-1.5.02s-.9-.05-1.01-.08c-.11-.03-.17-.12-.13-.24l.5-1.5s.04-.1.12-.15c.08-.05.19-.04.19-.04l2.1.02s.15-.01.23-.05c.08-.06.06-.18.06-.18l-.5-2.5s-.03-.15.01-.2c.04-.05.12-.05.19-.05l1.6-.02z"/>
                                        </svg>
                                    </a>
                                    <a href="#" class="social-link" aria-label="Telegram">
                                        <svg width="32" height="32" viewBox="0 0 24 24" fill="currentColor">
                                            <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm4.64 6.8c-.15 1.58-.8 5.42-1.13 7.19-.14.75-.42 1-.68 1.03-.58.05-1.02-.38-1.58-.75-.88-.58-1.38-.94-2.23-1.5-.99-.65-.35-1.01.22-1.59.15-.15 2.71-2.48 2.76-2.69a.2.2 0 00-.05-.18c-.06-.05-.14-.03-.21-.02-.09.02-1.49.95-4.22 2.79-.4.27-.76.41-1.08.4-.36-.01-1.04-.2-1.55-.37-.63-.2-1.13-.31-1.09-.66.02-.18.27-.36.74-.55 2.92-1.27 4.86-2.11 5.83-2.51 2.78-1.16 3.35-1.36 3.73-1.36.08 0 .27.02.39.12.1.08.13.19.14.27-.01.06.01.24 0 .38z"/>
                                        </svg>
                                    </a>
                                    <a href="#" class="social-link" aria-label="Instagram">
                                        <svg width="32" height="32" viewBox="0 0 24 24" fill="currentColor">
                                            <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
                                        </svg>
                                    </a>
                                </div>
                            </div>
                        </div>

                        <div class="contact-form-wrapper">
                            <h2 class="section-title">Напишите нам</h2>
                            <form @submit.prevent="handleSubmit" class="contact-form">
                                <div class="form-group">
                                    <label for="name" class="form-label">Ваше имя</label>
                                    <input 
                                        type="text" 
                                        id="name" 
                                        v-model="formData.name" 
                                        class="form-input" 
                                        placeholder="Иван Иванов"
                                        required
                                    />
                                </div>

                                <div class="form-group">
                                    <label for="email" class="form-label">Email</label>
                                    <input 
                                        type="email" 
                                        id="email" 
                                        v-model="formData.email" 
                                        class="form-input" 
                                        placeholder="ivan@example.com"
                                        required
                                    />
                                </div>

                                <div class="form-group">
                                    <label for="phone" class="form-label">Телефон</label>
                                    <input 
                                        type="tel" 
                                        id="phone" 
                                        v-model="formData.phone" 
                                        class="form-input" 
                                        placeholder="+7 (999) 123-45-67"
                                    />
                                </div>

                                <div class="form-group">
                                    <label for="message" class="form-label">Сообщение</label>
                                    <textarea 
                                        id="message" 
                                        v-model="formData.message" 
                                        class="form-textarea" 
                                        rows="5"
                                        placeholder="Ваше сообщение..."
                                        required
                                    ></textarea>
                                </div>

                                <button type="submit" class="submit-btn">
                                    Отправить сообщение
                                </button>
                            </form>
                        </div>
                    </div>
                </div>
            </section>
        </main>

        <Footer />
    </div>
</template>

<style scoped>
.contact-page {
    min-height: calc(100vh - 200px);
}

.hero-section {
    background: linear-gradient(135deg, #c49a6c 0%, #99582A 100%);
    padding: 80px 20px 60px;
    text-align: center;
    border-bottom: 4px solid #d7b389;
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

.contact-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 60px;
    align-items: start;
}

.section-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 32px;
    color: #3b2b1f;
    margin: 0 0 40px 0;
    font-weight: bold;
}

.contact-item {
    display: flex;
    gap: 20px;
    margin-bottom: 40px;
    align-items: flex-start;
}

.contact-icon {
    flex-shrink: 0;
    width: 60px;
    height: 60px;
    background: linear-gradient(135deg, #d7b389 0%, #c49a6c 100%);
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 4px 12px rgba(153, 88, 42, 0.2);
}

.contact-details {
    flex: 1;
}

.contact-label {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 18px;
    color: #3b2b1f;
    margin: 0 0 8px 0;
    font-weight: bold;
}

.contact-value {
    font-size: 16px;
    color: #5a4a3a;
    margin: 4px 0;
    line-height: 1.6;
}

.social-section {
    margin-top: 50px;
    padding-top: 40px;
    border-top: 2px solid #d7b389;
}

.social-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 20px;
    color: #3b2b1f;
    margin: 0 0 20px 0;
    font-weight: bold;
}

.social-links {
    display: flex;
    gap: 16px;
}

.social-link {
    width: 50px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(135deg, #d7b389 0%, #c49a6c 100%);
    border-radius: 12px;
    color: #3b2b1f;
    transition: all 0.3s ease;
    text-decoration: none;
    box-shadow: 0 4px 12px rgba(153, 88, 42, 0.2);
}

.social-link:hover {
    transform: translateY(-3px);
    box-shadow: 0 6px 20px rgba(153, 88, 42, 0.3);
    background: linear-gradient(135deg, #c49a6c 0%, #99582A 100%);
    color: white;
}

.contact-form-wrapper {
    background: white;
    padding: 40px;
    border-radius: 20px;
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.1);
    border: 2px solid #d7b389;
}

.contact-form {
    display: flex;
    flex-direction: column;
    gap: 24px;
}

.form-group {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.form-label {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 16px;
    color: #3b2b1f;
    font-weight: bold;
}

.form-input,
.form-textarea {
    padding: 14px 18px;
    border: 2px solid #d7b389;
    border-radius: 12px;
    font-size: 16px;
    font-family: inherit;
    color: #3b2b1f;
    background: #fffaf4;
    transition: all 0.3s ease;
}

.form-input:focus,
.form-textarea:focus {
    outline: none;
    border-color: #99582A;
    background: white;
    box-shadow: 0 0 0 3px rgba(153, 88, 42, 0.1);
}

.form-textarea {
    resize: vertical;
    min-height: 120px;
}

.submit-btn {
    padding: 16px 32px;
    background: linear-gradient(135deg, #99582A 0%, #c49a6c 100%);
    color: white;
    border: none;
    border-radius: 12px;
    font-family: "Dela Gothic One", sans-serif;
    font-size: 18px;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 12px rgba(153, 88, 42, 0.3);
    margin-top: 8px;
}

.submit-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(153, 88, 42, 0.4);
    background: linear-gradient(135deg, #c49a6c 0%, #99582A 100%);
}

.submit-btn:active {
    transform: translateY(0);
}

@media (max-width: 968px) {
    .contact-grid {
        grid-template-columns: 1fr;
        gap: 40px;
    }
    
    .hero-title {
        font-size: 36px;
    }
    
    .hero-subtitle {
        font-size: 18px;
    }
    
    .contact-form-wrapper {
        padding: 30px 20px;
    }
}

@media (max-width: 640px) {
    .hero-section {
        padding: 60px 15px 40px;
    }
    
    .hero-title {
        font-size: 28px;
    }
    
    .hero-subtitle {
        font-size: 16px;
    }
    
    .content-section {
        padding: 40px 15px;
    }
    
    .section-title {
        font-size: 24px;
    }
    
    .contact-item {
        flex-direction: column;
        gap: 12px;
    }
    
    .contact-icon {
        width: 50px;
        height: 50px;
    }
}
</style>

