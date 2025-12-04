<script setup>
import { ref, computed, inject } from 'vue';

const handleImageError = (event) => {
    event.target.src = 'data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAwIiBoZWlnaHQ9IjQwMCIgdmlld0JveD0iMCAwIDgwIDgwIiBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPjxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iNDAwIiBmaWxsPSIjZjVmNTVmNSIvPjxjaXJjbGUgY3g9IjIwMCIgY3k9IjIwMCIgcj0iMTUwIiBmaWxsPSIjZDdiMzg5IiBzdHJva2U9IiNjNDlhNmMiIHN0cm9rZS13aWR0aD0iNCIvPjxwYXRoIGQ9Ik0yMDAgMTAwIEwyNTAgMTc1IEwxNTAgMTc1IFoiIGZpbGw9IiM5OTU4MkEiLz48Y2lyY2xlIGN4PSIyMDAiIGN5PSIyMDAiIHI9IjQwIiBmaWxsPSIjYzQ5YTZjIi8+PC9zdmc+';
};

// Получаем состояние из родительского компонента
const activeCategory = inject('activeCategory', ref(2));
const searchQuery = inject('searchQuery', ref(''));
const setSearchQuery = inject('setSearchQuery', null);
const addToCartGlobal = inject('addToCart', null);

const allProducts = ref([
    // Пиццы
    {
        id: 1,
        categoryId: 2,
        additionalCategories: [7], // Новинка
        name: 'Пицца "4 Сыра"',
        description: 'Моцарелла, горгонзола, пармезан, чеддер',
        image: 'https://images.unsplash.com/photo-1574071318508-1cdbab80d002?w=400&h=400&fit=crop&q=80',
        prices: { small: 1790, large: 2190 },
        selectedSize: 'small',
        hasSizes: true
    },
    {
        id: 2,
        categoryId: 2,
        name: 'Классическая пицца',
        description: 'Томаты, моцарелла, базилик, орегано',
        image: 'https://images.unsplash.com/photo-1571997478779-2adcbbe9ab2f?w=400&h=400&fit=crop&q=80',
        prices: { small: 1450, large: 1850 },
        selectedSize: 'small',
        hasSizes: true
    },
    {
        id: 3,
        categoryId: 2,
        additionalCategories: [7], // Новинка
        name: 'Гавайская',
        description: 'Ветчина, ананас, моцарелла, соус',
        image: 'https://images.unsplash.com/photo-1604382354936-07c5d9983bd3?w=400&h=400&fit=crop&q=80',
        prices: { small: 1730, large: 2100 },
        selectedSize: 'small',
        hasSizes: true
    },
    {
        id: 4,
        categoryId: 2,
        name: 'Пепперони',
        description: 'Пепперони, моцарелла, томатный соус',
        image: 'https://images.unsplash.com/photo-1628840042765-356cda07504e?w=400&h=400&fit=crop&q=80',
        prices: { small: 1650, large: 2050 },
        selectedSize: 'small',
        hasSizes: true
    },
    {
        id: 5,
        categoryId: 2,
        name: 'Маргарита',
        description: 'Моцарелла, томаты, базилик',
        image: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?w=400&h=400&fit=crop&q=80',
        prices: { small: 1350, large: 1750 },
        selectedSize: 'small',
        hasSizes: true
    },
    {
        id: 6,
        categoryId: 2,
        name: 'Мясная',
        description: 'Ветчина, бекон, колбаса, моцарелла',
        image: 'https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?w=400&h=400&fit=crop&q=80',
        prices: { small: 1890, large: 2290 },
        selectedSize: 'small',
        hasSizes: true
    },
    // Напитки
    {
        id: 7,
        categoryId: 6,
        name: 'Кола',
        description: 'Освежающий газированный напиток',
        image: 'https://images.unsplash.com/photo-1554866585-cd94860890b7?w=400&h=400&fit=crop&q=80',
        prices: { single: 150 },
        selectedSize: 'single',
        hasSizes: false
    },
    {
        id: 8,
        categoryId: 6,
        name: 'Сок апельсиновый',
        description: 'Натуральный сок из апельсинов',
        image: 'https://images.unsplash.com/photo-1600271886742-f049cd451bba?w=400&h=400&fit=crop&q=80',
        prices: { single: 180 },
        selectedSize: 'single',
        hasSizes: false
    },
    {
        id: 9,
        categoryId: 6,
        additionalCategories: [7], // Новинка
        name: 'Лимонад',
        description: 'Домашний лимонад с мятой',
        image: 'https://images.unsplash.com/photo-1523677011781-c91d1bbe2fdc?w=400&h=400&fit=crop&q=80',
        prices: { single: 200 },
        selectedSize: 'single',
        hasSizes: false
    },
    {
        id: 10,
        categoryId: 6,
        name: 'Морс',
        description: 'Ягодный морс',
        image: 'https://images.unsplash.com/photo-1544145945-f90425340c7e?w=400&h=400&fit=crop&q=80',
        prices: { single: 190 },
        selectedSize: 'single',
        hasSizes: false
    },
    {
        id: 11,
        categoryId: 6,
        name: 'Чай',
        description: 'Горячий чай на выбор',
        image: 'https://images.unsplash.com/photo-1556679343-c7306c1976bc?w=400&h=400&fit=crop&q=80',
        prices: { single: 120 },
        selectedSize: 'single',
        hasSizes: false
    },
    {
        id: 12,
        categoryId: 6,
        name: 'Кофе',
        description: 'Ароматный кофе',
        image: 'https://images.unsplash.com/photo-1517487881594-2787fef5ebf7?w=400&h=400&fit=crop&q=80',
        prices: { single: 180 },
        selectedSize: 'single',
        hasSizes: false
    },
    // Закуски
    {
        id: 13,
        categoryId: 4,
        name: 'Картофель фри',
        description: 'Хрустящий картофель с соусом',
        image: 'https://images.unsplash.com/photo-1573080496219-bb080dd4f877?w=400&h=400&fit=crop&q=80',
        prices: { single: 250 },
        selectedSize: 'single',
        hasSizes: false
    },
    {
        id: 14,
        categoryId: 4,
        additionalCategories: [7], // Новинка
        name: 'Куриные крылышки',
        description: 'Острые куриные крылышки',
        image: 'https://images.unsplash.com/photo-1527477396000-e27163b481c2?w=400&h=400&fit=crop&q=80',
        prices: { single: 390 },
        selectedSize: 'single',
        hasSizes: false
    },
    {
        id: 15,
        categoryId: 4,
        name: 'Наггетсы',
        description: 'Куриные наггетсы 6 шт',
        image: 'https://images.unsplash.com/photo-1608039829570-6b3d9c269824?w=400&h=400&fit=crop&q=80',
        prices: { single: 320 },
        selectedSize: 'single',
        hasSizes: false
    },
    {
        id: 16,
        categoryId: 4,
        name: 'Сырные палочки',
        description: 'Хрустящие сырные палочки',
        image: 'https://images.unsplash.com/photo-1615367423051-73913e5a0cfe?w=400&h=400&fit=crop&q=80',
        prices: { single: 280 },
        selectedSize: 'single',
        hasSizes: false
    },
    // Десерты
    {
        id: 17,
        categoryId: 5,
        additionalCategories: [7], // Новинка
        name: 'Чизкейк',
        description: 'Нежный чизкейк с ягодами',
        image: 'https://images.unsplash.com/photo-1524351199678-941a58a3df50?w=400&h=400&fit=crop&q=80',
        prices: { single: 350 },
        selectedSize: 'single',
        hasSizes: false
    },
    {
        id: 18,
        categoryId: 5,
        name: 'Тирамису',
        description: 'Классический итальянский десерт',
        image: 'https://images.unsplash.com/photo-1571877227200-a0d98ea607e9?w=400&h=400&fit=crop&q=80',
        prices: { single: 380 },
        selectedSize: 'single',
        hasSizes: false
    },
    {
        id: 19,
        categoryId: 5,
        name: 'Мороженое',
        description: 'Мороженое на выбор',
        image: 'https://images.unsplash.com/photo-1563805042-7684c019e1b3?w=400&h=400&fit=crop&q=80',
        prices: { single: 200 },
        selectedSize: 'single',
        hasSizes: false
    },
    {
        id: 20,
        categoryId: 5,
        name: 'Брауни',
        description: 'Шоколадный брауни',
        image: 'https://images.unsplash.com/photo-1606313564200-e75d5e30476c?w=400&h=400&fit=crop&q=80',
        prices: { single: 280 },
        selectedSize: 'single',
        hasSizes: false
    },
    // Комбо
    {
        id: 21,
        categoryId: 1,
        additionalCategories: [7], // Новинка
        name: 'Комбо "Семейное"',
        description: '2 пиццы 35 см + напитки + картофель фри',
        image: 'https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?w=400&h=400&fit=crop&q=80',
        prices: { single: 2990 },
        selectedSize: 'single',
        hasSizes: false
    },
    {
        id: 22,
        categoryId: 1,
        name: 'Комбо "Друзья"',
        description: '3 пиццы 35 см + напитки + закуски',
        image: 'https://images.unsplash.com/photo-1574071318508-1cdbab80d002?w=400&h=400&fit=crop&q=80',
        prices: { single: 4290 },
        selectedSize: 'single',
        hasSizes: false
    },
    {
        id: 23,
        categoryId: 1,
        name: 'Комбо "Один"',
        description: 'Пицца 35 см + напиток + закуска',
        image: 'https://images.unsplash.com/photo-1513104890138-7c749659a591?w=400&h=400&fit=crop&q=80',
        prices: { single: 1790 },
        selectedSize: 'single',
        hasSizes: false
    }
]);

const filteredProducts = computed(() => {
    let filtered = allProducts.value;
    
    const query = searchQuery.value?.trim() || '';
    
    // Если есть поисковый запрос, ищем по всем категориям
    if (query) {
        const searchLower = query.toLowerCase();
        const searchWords = searchLower.split(/\s+/).filter(word => word.length > 0);
        
        filtered = filtered.filter(product => {
            const nameLower = product.name.toLowerCase();
            
            // Если одно слово - ищем вхождение в названии
            if (searchWords.length === 1) {
                return nameLower.includes(searchWords[0]);
            }
            
            // Если несколько слов - ищем все слова в названии (AND логика)
            return searchWords.every(word => nameLower.includes(word));
        });
        
        // Сортируем результаты по релевантности
        filtered.sort((a, b) => {
            const aName = a.name.toLowerCase();
            const bName = b.name.toLowerCase();
            
            // Подсчитываем релевантность только по названию
            const getRelevance = (name) => {
                let score = 0;
                const searchLower = query.toLowerCase();
                
                // Точное совпадение названия - максимальный приоритет
                if (name === searchLower) score += 100;
                
                // Название начинается с запроса
                else if (name.startsWith(searchLower)) score += 50;
                
                // Название содержит запрос
                else if (name.includes(searchLower)) score += 30;
                
                // Поиск по отдельным словам
                searchWords.forEach(word => {
                    if (name.startsWith(word)) score += 20;
                    else if (name.includes(word)) score += 15;
                });
                
                return score;
            };
            
            const aScore = getRelevance(aName);
            const bScore = getRelevance(bName);
            
            // Сначала по релевантности (убывание), потом по алфавиту
            if (bScore !== aScore) {
                return bScore - aScore;
            }
            return aName.localeCompare(bName, 'ru');
        });
    } else {
        // Если поиска нет, фильтруем по выбранной категории
        const category = activeCategory.value;
        if (category) {
            filtered = filtered.filter(product => {
                // Проверяем основную категорию
                if (product.categoryId === category) {
                    return true;
                }
                // Проверяем дополнительные категории
                if (product.additionalCategories && product.additionalCategories.includes(category)) {
                    return true;
                }
                return false;
            });
        }
    }
    
    return filtered;
});

const categoryTitles = {
    1: 'Комбо',
    2: 'Пиццы',
    4: 'Закуски',
    5: 'Десерты',
    6: 'Напитки',
    7: 'Новинки'
};

const handleSearchInput = (e) => {
    const value = e.target.value;
    if (setSearchQuery) {
        setSearchQuery(value);
    } else {
        searchQuery.value = value;
    }
};

const clearSearch = () => {
    if (setSearchQuery) {
        setSearchQuery('');
    } else {
        searchQuery.value = '';
    }
};

const selectSize = (productId, size) => {
    const product = allProducts.value.find(p => p.id === productId);
    if (product) {
        product.selectedSize = size;
    }
};

const getCurrentPrice = (product) => {
    if (product.hasSizes) {
        return product.prices[product.selectedSize];
    }
    return product.prices.single;
};

const animateToCart = (productCard, productImage) => {
    const cartIcon = document.getElementById('cart-icon');
    if (!cartIcon || !productCard || !productImage) return;

    const cartIconRect = cartIcon.getBoundingClientRect();
    const imageRect = productImage.getBoundingClientRect();

    // Создаем элемент для анимации
    const flyingElement = document.createElement('div');
    flyingElement.className = 'flying-product';
    flyingElement.style.position = 'fixed';
    flyingElement.style.width = '80px';
    flyingElement.style.height = '80px';
    flyingElement.style.borderRadius = '12px';
    flyingElement.style.overflow = 'hidden';
    flyingElement.style.zIndex = '10000';
    flyingElement.style.pointerEvents = 'none';
    flyingElement.style.boxShadow = '0 8px 24px rgba(0, 0, 0, 0.3)';
    flyingElement.style.border = '3px solid #d7b389';
    
    // Копируем изображение
    const img = document.createElement('img');
    img.src = productImage.src || productImage.getAttribute('src');
    img.style.width = '100%';
    img.style.height = '100%';
    img.style.objectFit = 'cover';
    flyingElement.appendChild(img);

    // Начальная позиция (центр изображения)
    const startX = imageRect.left + (imageRect.width / 2) - 40;
    const startY = imageRect.top + (imageRect.height / 2) - 40;
    
    flyingElement.style.left = startX + 'px';
    flyingElement.style.top = startY + 'px';
    flyingElement.style.opacity = '1';
    flyingElement.style.transform = 'scale(1) rotate(0deg)';

    document.body.appendChild(flyingElement);

    // Принудительный рефлоу для запуска анимации
    void flyingElement.offsetHeight;

    // Конечная позиция (центр иконки корзины)
    const endX = cartIconRect.left + (cartIconRect.width / 2) - 40;
    const endY = cartIconRect.top + (cartIconRect.height / 2) - 40;

    // Используем requestAnimationFrame для плавной анимации
    requestAnimationFrame(() => {
        flyingElement.style.transition = 'all 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94)';
        flyingElement.style.left = endX + 'px';
        flyingElement.style.top = endY + 'px';
        flyingElement.style.opacity = '0';
        flyingElement.style.transform = 'scale(0.2) rotate(180deg)';
    });

    // Удаляем элемент после анимации
    setTimeout(() => {
        if (flyingElement.parentNode) {
            flyingElement.parentNode.removeChild(flyingElement);
        }
    }, 800);
};

const addToCart = (product, event) => {
    // Находим карточку товара и изображение
    const button = event?.target;
    const productCard = button?.closest('.card');
    const productImage = productCard?.querySelector('.card-image');
    
    // Запускаем анимацию
    if (productCard && productImage) {
        // Небольшая задержка для плавности
        setTimeout(() => {
            animateToCart(productCard, productImage);
        }, 50);
    }

    let size = '';
    let sizeKey = '';
    if (product.hasSizes) {
        size = product.selectedSize === 'small' ? '35 см' : '45 см';
        sizeKey = product.selectedSize;
    } else {
        sizeKey = 'single';
    }
    const price = getCurrentPrice(product);
    
    const cartItem = {
        productId: product.id,
        name: product.name,
        image: product.image,
        size: sizeKey,
        sizeLabel: size,
        price: price,
        hasSizes: product.hasSizes
    };
    
    if (addToCartGlobal) {
        addToCartGlobal(cartItem);
        // Обновляем счетчик в Header
        window.dispatchEvent(new Event('cartUpdated'));
    } else {
        console.log(`Добавлено в корзину: ${product.name}${size ? `, размер: ${size}` : ''}, цена: ${price}₽`);
    }
};
</script>

<template>
    <section class="products">
        <div class="products-header">
            <h2 class="section-title">
                <span v-if="searchQuery && searchQuery.trim()">
                    Результаты поиска
                </span>
                <span v-else>
                    {{ categoryTitles[activeCategory] || 'Меню' }}
                </span>
            </h2>
            
            <div class="search-container">
                <div class="search-wrapper">
                    <svg class="search-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M21 21L15 15M17 10C17 13.866 13.866 17 10 17C6.13401 17 3 13.866 3 10C3 6.13401 6.13401 3 10 3C13.866 3 17 6.13401 17 10Z" stroke="#99582A" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    </svg>
                    <input
                        type="text"
                        class="search-input"
                        placeholder="Поиск по меню..."
                        :value="searchQuery"
                        @input="handleSearchInput"
                    />
                    <button 
                        v-if="searchQuery && searchQuery.trim()"
                        class="search-clear"
                        @click="clearSearch"
                        aria-label="Очистить поиск"
                    >
                        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <path d="M18 6L6 18M6 6L18 18" stroke="#99582A" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                        </svg>
                    </button>
                </div>
            </div>
        </div>
        
        <div v-if="filteredProducts.length === 0" class="no-results">
            <p>Ничего не найдено</p>
            <p class="no-results-hint">Попробуйте изменить поисковый запрос или выбрать другую категорию</p>
        </div>
        
        <div v-else class="products-grid">
            <div 
                v-for="product in filteredProducts" 
                :key="product.id"
                class="card"
            >
                <div class="card-image-wrapper">
                    <div class="image-overlay"></div>
                    <img 
                        :src="product.image" 
                        :alt="product.name"
                        class="card-image"
                        loading="lazy"
                        @error="handleImageError"
                    />
                    <div class="image-badge" v-if="product.id <= 6">Хит продаж</div>
                    <div class="image-badge image-badge-new" v-if="product.additionalCategories && product.additionalCategories.includes(7)">Новинка</div>
                </div>
                
                <div class="card-content">
                    <h3 class="card-title">{{ product.name }}</h3>
                    <p class="card-description">{{ product.description }}</p>
                    
                    <div class="size-selector" v-if="product.hasSizes">
                        <label class="size-label">Выберите размер:</label>
                        <div class="size-buttons">
                            <button
                                :class="['size-btn', { active: product.selectedSize === 'small' }]"
                                @click="selectSize(product.id, 'small')"
                            >
                                <span class="size-value">35 см</span>
                                <span class="size-price">{{ product.prices.small }}₽</span>
                            </button>
                            <button
                                :class="['size-btn', { active: product.selectedSize === 'large' }]"
                                @click="selectSize(product.id, 'large')"
                            >
                                <span class="size-value">45 см</span>
                                <span class="size-price">{{ product.prices.large }}₽</span>
                            </button>
                        </div>
                    </div>
                    
                    <div class="current-price">
                        <span class="price-label">Цена:</span>
                        <span class="price-value">{{ getCurrentPrice(product) }}₽</span>
                    </div>
                    
                    <button 
                        class="btn"
                        @click="addToCart(product, $event)"
                    >
                        Добавить в корзину
                    </button>
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

.products-header {
    margin-bottom: 40px;
}

.section-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 32px;
    color: #3b2b1f;
    text-align: center;
    margin-bottom: 30px;
    font-weight: bold;
}

.search-container {
    max-width: 600px;
    margin: 0 auto;
}

.search-wrapper {
    position: relative;
    display: flex;
    align-items: center;
}

.search-icon {
    position: absolute;
    left: 16px;
    z-index: 1;
    pointer-events: none;
}

.search-input {
    width: 100%;
    padding: 14px 50px 14px 48px;
    border: 2px solid #e8dcc6;
    border-radius: 16px;
    font-size: 16px;
    font-family: "Dela Gothic One", sans-serif;
    color: #3b2b1f;
    background: white;
    transition: all 0.3s ease;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
}

.search-input:focus {
    outline: none;
    border-color: #d7b389;
    box-shadow: 0 4px 12px rgba(153, 88, 42, 0.2);
}

.search-input::placeholder {
    color: #9ca3af;
}

.search-clear {
    position: absolute;
    right: 12px;
    background: transparent;
    border: none;
    cursor: pointer;
    padding: 4px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    transition: all 0.2s ease;
    z-index: 1;
}

.search-clear:hover {
    background: #f5e6d3;
    transform: scale(1.1);
}

.no-results {
    text-align: center;
    padding: 60px 20px;
    color: #6a5b4a;
}

.no-results p {
    font-size: 20px;
    font-family: "Dela Gothic One", sans-serif;
    margin: 0 0 12px 0;
    color: #3b2b1f;
}

.no-results-hint {
    font-size: 14px;
    color: #6a5b4a;
    font-family: sans-serif;
}

.products-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 30px;
}

.card {
    background: white;
    border-radius: 24px;
    overflow: hidden;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
    transition: all 0.3s ease;
    display: flex;
    flex-direction: column;
    border: 2px solid transparent;
}

.card:hover {
    transform: translateY(-8px);
    box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
    border-color: #d7b389;
}

.card-image-wrapper {
    width: 100%;
    padding-top: 100%;
    position: relative;
    background: linear-gradient(135deg, #fffaf4 0%, #f5e6d3 100%);
    overflow: hidden;
    border-bottom: 3px solid #c49a6c;
}

.image-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(
        180deg, 
        rgba(215, 179, 137, 0.15) 0%, 
        transparent 40%,
        transparent 60%,
        rgba(153, 88, 42, 0.25) 100%
    );
    z-index: 1;
    pointer-events: none;
}

.card-image {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
    transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
    filter: 
        brightness(1.1) 
        contrast(1.15) 
        saturate(1.25)
        sepia(0.08)
        hue-rotate(-5deg);
    transform: scale(1);
    background-color: #f5e6d3;
}

.card:hover .card-image {
    transform: scale(1.1);
    filter: 
        brightness(1.2) 
        contrast(1.2) 
        saturate(1.3)
        sepia(0.1)
        hue-rotate(-5deg);
}

.image-badge {
    position: absolute;
    top: 12px;
    right: 12px;
    background: linear-gradient(135deg, #99582A 0%, #c49a6c 100%);
    color: white;
    padding: 6px 12px;
    border-radius: 20px;
    font-size: 12px;
    font-weight: bold;
    font-family: "Dela Gothic One", sans-serif;
    z-index: 2;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

.image-badge-new {
    background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%);
    animation: pulse 2s ease-in-out infinite;
    top: 12px;
    left: 12px;
    right: auto;
}

@keyframes pulse {
    0%, 100% {
        transform: scale(1);
        box-shadow: 0 2px 8px rgba(231, 76, 60, 0.3);
    }
    50% {
        transform: scale(1.05);
        box-shadow: 0 4px 12px rgba(231, 76, 60, 0.5);
    }
}

.card-content {
    padding: 24px;
    display: flex;
    flex-direction: column;
    flex: 1;
    gap: 16px;
}

.card-title {
    font-family: "Dela Gothic One", sans-serif;
    font-size: 22px;
    color: #3b2b1f;
    margin: 0;
    font-weight: bold;
    line-height: 1.3;
}

.card-description {
    font-size: 14px;
    color: #6a5b4a;
    margin: 0;
    line-height: 1.6;
    flex: 1;
}

.size-selector {
    margin: 8px 0;
}

.size-label {
    display: block;
    font-size: 13px;
    color: #6a5b4a;
    font-weight: 600;
    margin-bottom: 10px;
    font-family: "Dela Gothic One", sans-serif;
}

.size-buttons {
    display: flex;
    gap: 8px;
}

.size-btn {
    flex: 1;
    padding: 10px 12px;
    background: #f5e6d3;
    border: 2px solid #e8dcc6;
    border-radius: 12px;
    cursor: pointer;
    transition: all 0.3s ease;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 4px;
    font-family: "Dela Gothic One", sans-serif;
}

.size-btn:hover {
    background: #e8dcc6;
    border-color: #d7b389;
    transform: translateY(-2px);
}

.size-btn.active {
    background: linear-gradient(135deg, #d7b389 0%, #c49a6c 100%);
    border-color: #99582A;
    color: #3b2b1f;
    box-shadow: 0 4px 12px rgba(153, 88, 42, 0.3);
}

.size-value {
    font-size: 14px;
    font-weight: bold;
    color: inherit;
}

.size-price {
    font-size: 12px;
    color: inherit;
    opacity: 0.9;
}

.current-price {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px 16px;
    background: linear-gradient(135deg, #fffaf4 0%, #f5e6d3 100%);
    border-radius: 12px;
    border: 2px solid #e8dcc6;
    margin: 8px 0;
}

.price-label {
    font-size: 14px;
    color: #6a5b4a;
    font-weight: 600;
    font-family: "Dela Gothic One", sans-serif;
}

.price-value {
    font-size: 24px;
    color: #99582A;
    font-weight: bold;
    font-family: "Dela Gothic One", sans-serif;
}

.btn {
    margin-top: auto;
    padding: 14px 24px;
    background: linear-gradient(135deg, #d7b389 0%, #c49a6c 100%);
    color: #3b2b1f;
    border: none;
    border-radius: 14px;
    font-weight: bold;
    font-size: 16px;
    font-family: "Dela Gothic One", sans-serif;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 12px rgba(153, 88, 42, 0.25);
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

.btn:hover {
    background: linear-gradient(135deg, #c49a6c 0%, #99582A 100%);
    color: white;
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(153, 88, 42, 0.4);
}

.btn:active {
    transform: translateY(0);
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
        grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
        gap: 20px;
    }
    
    .card-content {
        padding: 20px;
    }
    
    .size-buttons {
        flex-direction: column;
    }
    
    .size-btn {
        width: 100%;
    }
}

@media (max-width: 480px) {
    .products-grid {
        grid-template-columns: 1fr;
    }
    
    .card-title {
        font-size: 20px;
    }
    
    .price-value {
        font-size: 20px;
    }
}
</style>
