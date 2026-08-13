<template>
    <div class="layout layout--default">
        <div class="layout__background" aria-hidden="true"></div>
        <Header />

        <MenuSidebar />

        <CartSidebar />

        <UsernameModal />

        <div class="w-100 container--fluid">
            <slot />
        </div>

        <Footer />
    </div>
</template>

<style lang="scss" scoped>
@use "~/assets/styles/settings" as *;

.layout {
    position: relative;
    width: 100%;
    overflow: hidden;
    &--default {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        min-height: 100vh;
    }

    &__background {
        position: fixed;
        z-index: -1;
        inset: 0;
        background:
            linear-gradient(
                to bottom,
                rgba(19, 19, 20, 0.2),
                rgba(19, 19, 20, 0.92)
            ),
            url("https://lh3.googleusercontent.com/aida-public/AB6AXuCtqd6FsqeHQ8uhu02PguKF4aCm6EdTx-tO4Nu2EKHPmrRCckpQZOkPkXAk0Y4KXwDEeETuy4YKvBb_BjOD20T_FvOaJZ9iBvDGEz48WTNkHky6LC3aqjUTt6TGObmbK_GEKjmc3J8ThR1PA-ykuimMsRSKKjzMEVn8qqzBE_nDNJNcxC66mSRQh8Uw9n3Ql1vrBI-dUhtbsjWel5uHXw8ozr9pOYaqavKPF07K0PHfq_WFTOIy_SUj_-MoodsIA_iqoKdnR2ofvVk")
                center / cover;
        opacity: 0.24;
        transform: scale(1.04);
        pointer-events: none;
    }
}
</style>
