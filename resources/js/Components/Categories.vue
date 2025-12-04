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
    background: #c9a982;
    padding: 20px 0;
    margin: 0;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
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
    color: #3b2b1f;
    transition: all 0.3s ease;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}

.category-btn:hover {
    background: #f5e6d3;
    transform: translateY(-2px);
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
}

.category-btn.active {
    background: #99582A;
    color: #fff;
    border-color: #c49a6c;
    box-shadow: 0 4px 12px rgba(153, 88, 42, 0.3);
}

.category-btn.active:hover {
    background: #8a4d25;
}

@media (max-width: 768px) {
    .categories-container {
        padding: 0 15px;
        gap: 8px;
    }
    
    .category-btn {
        padding: 8px 18px;
        font-size: 13px;
    }
}
</style>
