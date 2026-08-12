<template>
    <Hero
        title="Support the Prison"
        subtitle="Purchases directly support server hosting, custom plugin development, and new weekly updates. Thank you for keeping the dream alive!"
        image="https://lh3.googleusercontent.com/aida-public/AB6AXuCtqd6FsqeHQ8uhu02PguKF4aCm6EdTx-tO4Nu2EKHPmrRCckpQZOkPkXAk0Y4KXwDEeETuy4YKvBb_BjOD20T_FvOaJZ9iBvDGEz48WTNkHky6LC3aqjUTt6TGObmbK_GEKjmc3J8ThR1PA-ykuimMsRSKKjzMEVn8qqzBE_nDNJNcxC66mSRQh8Uw9n3Ql1vrBI-dUhtbsjWel5uHXw8ozr9pOYaqavKPF07K0PHfq_WFTOIy_SUj_-MoodsIA_iqoKdnR2ofvVk"
        class="mb-10"
    >
        <template #eyebrow>Official Server Store</template>
    </Hero>

    <div class="container">
        <div v-if="categories && categories.length > 1" class="category-tabs">
            <NuxtLink
                v-for="category in categories"
                :key="category.id"
                class="category-link"
                :to="{ hash: `#${titleCase(category.name)}` }"
            >
                {{ category.name }}
            </NuxtLink>
        </div>

        <section
            v-for="category in categories"
            :key="category.id"
            :id="titleCase(category.name)"
            class="category"
        >
            <div class="category-heading">
                <span>Store Category</span>
                <h2>{{ category.name }}</h2>
            </div>

            <div class="row">
                <div
                    v-for="pkg in category.packages"
                    :key="pkg.id"
                    class="col-12 col-sm-6 col-md-4 col-lg-3"
                >
                    <PackageCard
                        :pkg="pkg"
                        :row="category.packages.length === 1"
                        hide-options
                    />
                </div>
            </div>
        </section>
    </div>

    <NuxtPage />
</template>

<script lang="ts" setup>
useSeoMeta({
    ogTitle: "PurplePrison Store",
    description: "Support PurplePrison and upgrade your Minecraft experience.",
    ogDescription:
        "Support PurplePrison and upgrade your Minecraft experience.",
    ogImage: "/purpleprison-logo-full.png",
    twitterCard: "summary_large_image",
});

const categoryStore = useCategoryStore();
const { data: categories } = await useAsyncData("categories", () => {
    return categoryStore.fetchCategories();
});
</script>

<style scoped lang="scss">
.category-tabs {
    display: flex;
    gap: 12px;
    overflow-x: auto;
    padding: 8px 4px 22px;
    margin-bottom: 26px;
    scrollbar-width: thin;
}

.category-link {
    display: block;
    white-space: nowrap;
    padding: 11px 22px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 10px;
    background: rgba(32, 31, 32, 0.68);
    color: rgba(255, 255, 255, 0.65);
    font-family: Rajdhani, sans-serif;
    font-weight: 700;
    letter-spacing: 0.13em;
    text-transform: uppercase;
    text-decoration: none;
    transition: 180ms ease;

    &:hover {
        color: #181818;
        background: #f2ca50;
        border-color: #f2ca50;
        box-shadow: 0 0 20px rgba(242, 202, 80, 0.28);
    }
}

.category {
    margin-bottom: 68px;

    &-heading {
        margin: 0 0 24px;
        text-align: center;

        span {
            color: #f2ca50;
            font-family: Rajdhani, sans-serif;
            font-size: 12px;
            font-weight: 700;
            letter-spacing: 0.2em;
            text-transform: uppercase;
        }

        h2 {
            margin: 5px 0 0;
            color: #fff;
            font-family: Orbitron, sans-serif;
            font-size: clamp(1.45rem, 3vw, 2.15rem);
            text-transform: uppercase;
        }
    }

    :deep(.package-card) {
        animation: card-reveal 500ms ease both;
    }
    :deep(.col-12:nth-child(2) .package-card) {
        animation-delay: 60ms;
    }
    :deep(.col-12:nth-child(3) .package-card) {
        animation-delay: 120ms;
    }
    :deep(.col-12:nth-child(4) .package-card) {
        animation-delay: 180ms;
    }
}

@keyframes card-reveal {
    from {
        opacity: 0;
        transform: translateY(12px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}
</style>
