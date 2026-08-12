<template>
    <div class="category-card">
        <div class="category-card__image">
            <NuxtImg
                :src="image"
                :alt="$t('category.image_alt', { name: category.name })"
                width="80px"
                height="80px"
            />
        </div>

        <div class="category-card__header">
            <h4>{{ category.name }}</h4>
        </div>
    </div>
</template>

<script setup lang="ts">
import type { Category } from "~/types";

interface CategoryCardProps {
    image: string;
    category: Category;
}

defineProps<CategoryCardProps>();
</script>

<style lang="scss" scoped>
@use "~/assets/styles/settings" as *;

.category-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    aspect-ratio: 1/ 1;
    padding: 18px;
    border-radius: $category-card-border-radius;
    border: $category-card-border;
    background: $category-card-bg;
    box-shadow: 0 14px 28px rgba(0, 0, 0, 0.2);
    transition:
        transform 180ms ease,
        border-color 180ms ease,
        box-shadow 180ms ease;
    min-width: $category-card-min-width;

    &__image {
        margin-bottom: 14px;
    }

    &__header h4 {
        margin: 0;
        font-size: 1.05rem;
        letter-spacing: -0.01em;
        color: $text-high-emphasis-color;
    }

    &:hover {
        transform: translateY(-3px);
        border-color: rgba(215, 162, 74, 0.65);
        box-shadow: 0 18px 36px rgba(0, 0, 0, 0.3);
    }

    img {
        object-fit: contain;
    }
}
</style>
