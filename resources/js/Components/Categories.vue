<template>
    <section class="categories">
        <div class="categories-container">
            <button 
                v-for="category in categories" 
                :key="category.id"
                :class="['category-btn', { active: activeCategory === category.id }]"
                @click="selectCategory(category.id)"
            >
                {{ category.name }}
            </button>
        </div>
    </section>
</template>

<script setup>
import { ref, inject } from 'vue';

const setActiveCategory = inject('setActiveCategory', null);
const activeCategory = inject('activeCategory', ref(2));

const categories = [
    { id: 1, name: 'Комбо' },
    { id: 2, name: 'Пиццы' },
    { id: 4, name: 'Закуски' },
    { id: 5, name: 'Десерты' },
    { id: 6, name: 'Напитки' },
    { id: 7, name: 'Новинки' },
];

const selectCategory = (id) => {
    if (setActiveCategory) {
        setActiveCategory(id);
    } else {
        activeCategory.value = id;
    }
};
</script>

<style scoped>
.categories {
    background: linear-gradient(135deg, #C85D3E 0%, #B84A3A 100%);
    padding: 20px 0;
    margin: 0;
    box-shadow: 0 2px 12px rgba(200, 93, 62, 0.15);
}

.categories-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    display: flex;
    justify-content: center;
    gap: 12px;
    flex-wrap: wrap;
}

.category-btn {
    padding: 10px 24px;
    background: #fff;
    border: 2px solid transparent;
    border-radius: 25px;
    cursor: pointer;
    font-weight: 600;
    font-size: 15px;
    font-family: "Dela Gothic One", sans-serif;
    color: #3D2E28;
    transition: all 0.3s ease;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}

.category-btn:hover {
    background: rgba(245, 240, 232, 0.8);
    transform: translateY(-2px);
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
}

.category-btn.active {
    background: rgba(255, 255, 255, 0.95);
    color: #B84A3A;
    border-color: rgba(255, 255, 255, 0.5);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.category-btn.active:hover {
    background: rgba(255, 255, 255, 1);
}

@media (max-width: 968px) {
    .categories-container {
        padding: 0 18px;
        gap: 10px;
    }
    
    .category-btn {
        padding: 9px 20px;
        font-size: 14px;
    }
}

@media (max-width: 768px) {
    .categories {
        padding: 18px 0;
    }
    
    .categories-container {
        padding: 0 15px;
        gap: 8px;
    }
    
    .category-btn {
        padding: 8px 18px;
        font-size: 13px;
    }
}

@media (max-width: 640px) {
    .categories {
        padding: 15px 0;
    }
    
    .categories-container {
        padding: 0 12px;
        gap: 6px;
    }
    
    .category-btn {
        padding: 7px 14px;
        font-size: 12px;
    }
}

@media (max-width: 480px) {
    .categories {
        padding: 12px 0;
    }
    
    .categories-container {
        padding: 0 10px;
        gap: 5px;
    }
    
    .category-btn {
        padding: 6px 12px;
        font-size: 11px;
    }
}
</style>
