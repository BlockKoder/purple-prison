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
    .replaceAll('href="/purpleprison-home/"', 'href="/" target="_top"')
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
