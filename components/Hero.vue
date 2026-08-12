<template>
    <div class="hero">
        <div class="hero__background">
            <img class="hero__image" :src="image" :alt="title" loading="lazy" />
        </div>
        <div class="hero__title">
            <span v-if="$slots.eyebrow" class="hero__eyebrow"
                ><slot name="eyebrow"
            /></span>
            <h1>{{ title }}</h1>
            <div>{{ subtitle }}</div>
        </div>
    </div>
</template>

<script setup lang="ts">
interface HeroProps {
    title: string;
    subtitle: string;
    image: string;
}

defineProps<HeroProps>();
</script>

<style lang="scss" scoped>
@use "~/assets/styles/settings" as *;

.hero {
    position: relative;
    width: 100%;
    height: $hero-banner-height;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    border-radius: $hero-banner-border-radius;
    overflow: hidden;

    @if ($hero-gradient) {
        &::after {
            content: "";
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: $hero-gradient;
            z-index: 1;
        }
    }

    &__title {
        max-width: 760px;
        padding: 0 24px;

        h1 {
            color: inherit;
            font-size: clamp(2rem, 6vw, 4rem);
            font-family: Orbitron, sans-serif;
            font-weight: 800;
            letter-spacing: -0.06em;
            text-transform: uppercase;
            text-shadow:
                3px 3px 0 rgba(0, 0, 0, 0.75),
                0 0 30px rgba(242, 202, 80, 0.35);
            margin-bottom: 10px;
            text-wrap: balance;
        }

        div {
            font-size: clamp(1rem, 2vw, 1.25rem);
            color: rgba(255, 255, 255, 0.7);
            font-family: Rajdhani, sans-serif;
            max-width: 60ch;
            margin: 0 auto;
        }

        color: $hero-banner-color;
        position: relative;
        z-index: 2;
        animation: hero-fade-in 650ms ease-out both;
    }

    &__eyebrow {
        display: inline-block;
        margin-bottom: 18px;
        padding: 7px 14px;
        border: 1px solid rgba(242, 202, 80, 0.4);
        border-radius: 999px;
        color: #f2ca50;
        background: rgba(242, 202, 80, 0.07);
        font-family: Rajdhani, sans-serif;
        font-size: 12px;
        font-weight: 700;
        letter-spacing: 0.19em;
    }

    &__background {
        position: absolute;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        opacity: $hero-background-opacity;
    }

    &__image {
        width: 100%;
        height: 100%;
        object-fit: cover;
        transform: scale(1.05);
        animation: hero-pan 16s ease-in-out infinite alternate;
    }
}

@keyframes hero-fade-in {
    from {
        opacity: 0;
        transform: translateY(18px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes hero-pan {
    from {
        transform: scale(1.05) translateX(-1.5%);
    }

    to {
        transform: scale(1.08) translateX(1.5%);
    }
}
</style>
