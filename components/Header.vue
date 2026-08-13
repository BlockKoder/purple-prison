<template>
    <header class="store-header">
        <div class="container">
            <nav class="store-header__nav">
                <a :href="appConfig.mainSiteUrl" class="store-header__brand">
                    <img src="/nav-logo.png" :alt="$t('store_name')" />
                </a>
                <div class="store-header__links">
                    <a href="/">Home</a>
                    <a class="active" href="#top">Store</a>
                    <a href="/features.html">Play</a>
                    <a href="/vote.html">Vote</a>
                    <a href="/wiki.html">Wiki</a>
                </div>
                <div class="store-header__actions">
                    <NuxtLink
                        class="store-header__login"
                        :to="authStore.loginRoute"
                        >{{
                            authStore.isAuthenticated
                                ? authStore.user.username
                                : $t("buttons.login")
                        }}</NuxtLink
                    >
                    <button
                        class="store-header__cart"
                        @click="uiStore.toggleItem('cart-sidebar')"
                    >
                        <Icon name="cart" width="18" /><span>Cart</span
                        ><b>{{ basketStore.basket?.packages?.length ?? 0 }}</b>
                    </button>
                </div>
                <button
                    class="store-header__mobile-cart"
                    @click="uiStore.toggleItem('cart-sidebar')"
                    aria-label="Open cart"
                >
                    <Icon name="cart" width="20" /><b>{{
                        basketStore.basket?.packages?.length ?? 0
                    }}</b>
                </button>
            </nav>
        </div>
    </header>
</template>

<script setup lang="ts">
const uiStore = useUIStore();
const authStore = useAuthStore();
const basketStore = useBasketStore();
const appConfig = useAppConfig();
</script>

<style lang="scss" scoped>
.store-header {
    position: sticky;
    top: 0;
    z-index: 600;
    padding: 16px 0;
    background: linear-gradient(to bottom, rgba(19, 19, 20, 0.92), transparent);
}
.store-header__nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    min-height: 72px;
    padding: 12px 20px;
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 16px;
    background: rgba(32, 31, 32, 0.7);
    backdrop-filter: blur(20px);
    box-shadow: 0 18px 40px rgba(0, 0, 0, 0.28);
}
.store-header__brand img {
    display: block;
    width: auto;
    height: 42px;
    max-width: 190px;
    object-fit: contain;
}
.store-header__links,
.store-header__actions {
    display: flex;
    align-items: center;
    gap: 24px;
}
.store-header__links a,
.store-header__login {
    position: relative;
    color: #bbb6b8;
    font-family: Rajdhani, sans-serif;
    font-size: 14px;
    font-weight: 700;
    letter-spacing: 0.13em;
    text-decoration: none;
    text-transform: uppercase;
    transition: color 0.2s;
}
.store-header__links a:hover,
.store-header__links .active,
.store-header__login:hover {
    color: #fff;
}
.store-header__links .active::after {
    content: "";
    position: absolute;
    left: 50%;
    bottom: -7px;
    width: 100%;
    height: 2px;
    background: #ec4899;
    transform: translateX(-50%);
}
.store-header__cart {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 10px 13px;
    border: 0;
    border-radius: 10px;
    color: #171717;
    background: #f2ca50;
    font:
        700 13px Rajdhani,
        sans-serif;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    cursor: pointer;
}
.store-header__cart b,
.store-header__mobile-cart b {
    display: grid;
    place-items: center;
    min-width: 18px;
    height: 18px;
    border-radius: 999px;
    color: #fff;
    background: #7c3aed;
    font-size: 11px;
}
.store-header__mobile-cart {
    display: none;
    align-items: center;
    gap: 7px;
    padding: 9px;
    border: 1px solid rgba(255, 255, 255, 0.12);
    border-radius: 10px;
    color: #fff;
    background: transparent;
}
@media (max-width: 960px) {
    .store-header__links,
    .store-header__actions {
        display: none;
    }
    .store-header__mobile-cart {
        display: flex;
    }
    .store-header__nav {
        min-height: 60px;
    }
    .store-header__brand img {
        height: 34px;
    }
}
</style>
