<template>
    <li>
        <img :src="props.woman.image" :alt="'Imagem de perfil da ' + props.woman.name" />
        <details>
            <summary>{{ props.woman.name }}</summary>
            <p>{{ props.woman.desc }}</p>
        </details>
    </li>
</template>
<script setup lang="ts">
import type { Woman } from '../model/Woman';
const props = defineProps<{ woman: Woman }>();
</script>
<style scoped>
li {
    color: #fdfdfd;
    background-color: var(--main-color);
    border-radius: 30px;
    width: 250px;
    display: grid;
    place-items: center;
    gap: 1rem;
    padding: 1.5rem;
}

img {
    border-radius: 100%;
    width: 130px;
    min-height: 130px;
    height: 130px;
}

details p {
    font-size: 13px;
}
</style>
