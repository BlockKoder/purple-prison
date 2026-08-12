<template>
    <iframe
        class="purpleprison-home"
        :srcdoc="homeDocument"
        title="PurplePrison"
    ></iframe>
</template>

<script setup lang="ts">
definePageMeta({ layout: false });

import rawHomeDocument from "~/assets/purpleprison-home.html?raw";

const homeDocument = rawHomeDocument
    .replace("<head>", '<head><base href="/">')
    .replaceAll('href="/purpleprison-home/"', 'href="/"')
    .replaceAll('href="login.html"', 'href="/login"')
    .replaceAll('href="register.html"', 'href="/register"')
    .replaceAll('href="features.html"', 'href="/features"')
    .replaceAll('href="vote.html"', 'href="/vote"')
    .replaceAll('href="wiki.html"', 'href="/wiki"')
    .replaceAll('href="staff.html"', 'href="/staff"')
    .replaceAll('href="support.html"', 'href="/support"')
    .replaceAll('href="contact.html"', 'href="/contact"')
    .replaceAll('href="privacy.html"', 'href="/privacy"')
    .replaceAll('href="terms.html"', 'href="/terms"')
    .replaceAll('href="store.html"', 'href="/store"')
    .replaceAll("<a ", '<a target="_top" ');
</script>

<style scoped>
.purpleprison-home {
    display: block;
    width: 100%;
    height: 100vh;
    height: 100dvh;
    border: 0;
}
</style>
