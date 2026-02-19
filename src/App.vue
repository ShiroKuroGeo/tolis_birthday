<script setup>
import { ref } from 'vue'
import Opening from './Opening.vue'
import Main from './Main.vue'

const active = ref(false)
</script>

<template>
    <div>
        <Opening v-if="!active" @enterSite="active = true" />

        <Main v-if="active" />
    </div>
</template>