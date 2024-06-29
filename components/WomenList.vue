<template>
    <ul>
        <WomanCard v-for="woman in women" :key="woman._id" :woman="woman" />
    </ul>
</template>
<script setup lang="ts">
import type { Woman } from '../model/Woman';

const { data } = await useFetch('https://backend-teste-vn7a.onrender.com/mulheres', {});
const women: Woman[] | unknown = data.value;
</script>
<style scoped>
ul {
    max-width: 1280px;
    margin: 0 auto;
    padding: 3rem 0;
    display: flex;
    gap: 2rem;
    justify-content: center;
    align-items: flex-start;
    list-style: none;
    flex-wrap: wrap;
}
</style>
