<template>
    <div class="container mx-auto rounded-xl shadow border p-8 m-10">
        <MainComponent></MainComponent>
    </div>
</template>

<script>

import MainComponent from "@/components/Main.vue";

export default {
    name: 'App',
    components: {
        MainComponent
    }
}
</script>

<style lang="scss">
html {
    background: #262626;

    body {
        max-width: 1920px;
        max-height: 950px;
    }
}
</style>
