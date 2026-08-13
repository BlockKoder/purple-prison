<template>
    <iframe
        v-if="pageDocument"
        class="purpleprison-page"
        :srcdoc="pageDocument"
        :title="`${routeName} | PurplePrison`"
    ></iframe>
    <div v-else class="not-found">Page not found.</div>
</template>

<script setup lang="ts">
import contactDocument from "~/assets/purpleprison-pages/contact.html?raw";
import featuresDocument from "~/assets/purpleprison-pages/features.html?raw";
import loginDocument from "~/assets/purpleprison-pages/login.html?raw";
import privacyDocument from "~/assets/purpleprison-pages/privacy.html?raw";
import registerDocument from "~/assets/purpleprison-pages/register.html?raw";
import staffDocument from "~/assets/purpleprison-pages/staff.html?raw";
import supportDocument from "~/assets/purpleprison-pages/support.html?raw";
import termsDocument from "~/assets/purpleprison-pages/terms.html?raw";
import voteDocument from "~/assets/purpleprison-pages/vote.html?raw";
import wikiDocument from "~/assets/purpleprison-pages/wiki.html?raw";

definePageMeta({ layout: false });

const route = useRoute();
const routeName = computed(() => String(route.params.slug));

const pages: Record<string, string> = {
    contact: contactDocument,
    features: featuresDocument,
    login: loginDocument,
    privacy: privacyDocument,
    register: registerDocument,
    staff: staffDocument,
    support: supportDocument,
    terms: termsDocument,
    vote: voteDocument,
    wiki: wikiDocument,
};

const pageDocument = computed(() => {
    const document = pages[routeName.value];

    if (!document) return null;

    return document
        .replace("<head>", '<head><base href="/">')
        .replaceAll(
            "https://headless-template.pages.dev",
            "https://purpleprison.pages.dev/",
        )
        .replaceAll(
            "https://tebex-headless-template.pages.dev",
            "https://purpleprison.pages.dev/",
        )
        .replaceAll('href="index.html"', 'href="/"')
        .replaceAll('href="store.html"', 'href="/store"')
        .replaceAll('href="features.html"', 'href="/features"')
        .replaceAll('href="vote.html"', 'href="/vote"')
        .replaceAll('href="wiki.html"', 'href="/wiki"')
        .replaceAll('href="staff.html"', 'href="/staff"')
        .replaceAll('href="support.html"', 'href="/support"')
        .replaceAll('href="contact.html"', 'href="/contact"')
        .replaceAll('href="login.html"', 'href="/login"')
        .replaceAll('href="register.html"', 'href="/register"')
        .replaceAll('href="privacy.html"', 'href="/privacy"')
        .replaceAll('href="terms.html"', 'href="/terms"')
        .replaceAll("<a ", '<a target="_top" ');
});
</script>

<style scoped>
.purpleprison-page {
    display: block;
    width: 100%;
    height: 100vh;
    height: 100dvh;
    border: 0;
}

.not-found {
    display: grid;
    min-height: 100vh;
    place-items: center;
    color: white;
}
</style>
