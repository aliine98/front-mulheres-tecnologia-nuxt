<template>
    <li class="woman-card">
        <button class="delete-btn" @click="deleteWoman(props.woman._id)"><img src="../assets/delete.png" width="45" alt="Delete icon" /></button>
        <img :src="props.woman.image" :alt="'Imagem de perfil da ' + props.woman.name" class="woman-img" />
        <details>
            <summary>{{ props.woman.name }}</summary>
            <p class="woman-description">{{ props.woman.desc }}</p>
        </details>
        <button class="secondary-btn" @click="openDialog">Editar</button>
        <dialog ref="dialog" class="edit-dialog">
            <button class="close-btn" @click="closeDialog"><img src="../assets/cross.svg" width="20" alt="close icon" /></button>
            <form @submit.prevent="updateWoman(name, image, desc, props.woman._id)">
                <label>Nome: <input type="text" v-model="name" class="form-input" /></label>
                <label>Url da imagem: <input type="text" v-model="image" class="form-input" /></label>
                <label>Descrição: <textarea v-model="desc" class="form-input" rows="5"></textarea></label>
                <button type="submit" class="primary-btn" :disabled>Atualizar</button>
            </form>
        </dialog>
    </li>
</template>
<script setup lang="ts">
import { ref } from 'vue';
import type { Woman } from '../model/Woman';
const props = defineProps<{ woman: Woman }>();
const dialog = ref(null);
const name = ref(null);
const image = ref(null);
const desc = ref(null);
const disabled = ref(false);

function openDialog() {
    dialog.value!.showModal();
}

function closeDialog() {
    dialog.value!.close();
}

async function updateWoman(name: string | null, image: string | null, desc: string | null, id: string | undefined) {
    disabled.value = true;
    const body = {};
    if (name) body.name = name;
    if (image) body.image = image;
    if (desc) body.desc = desc;

    await $fetch(`https://backend-teste-vn7a.onrender.com/mulheres/${id}`, { method: 'PATCH', body });
    reloadNuxtApp();
}

async function deleteWoman(id: string | undefined) {
    await $fetch(`https://backend-teste-vn7a.onrender.com/mulheres/${id}`, { method: 'DELETE' });
    reloadNuxtApp();
}
</script>
<style scoped>
.woman-card {
    color: #fdfdfd;
    background-color: var(--main-color);
    border-radius: 30px;
    width: 250px;
    display: grid;
    place-items: center;
    gap: 1rem;
    padding: 1.5rem;
    position: relative;
}

.delete-btn,
.close-btn {
    position: absolute;
    background: none;
    border: transparent;
    transition: all 0.5s;
    cursor: pointer;
}

.delete-btn {
    top: -16px;
    right: -16px;
}

.close-btn {
    top: 5px;
    right: 5px;
}

.delete-btn:hover {
    filter: brightness(80%);
}

.woman-img {
    border-radius: 100%;
    width: 130px;
    min-height: 130px;
    height: 130px;
}

.woman-description {
    font-size: 13px;
}

.form-input {
    display: block;
    border-radius: 10px;
    border: 2px solid var(--main-color);
    width: 100%;
    padding: 8px;
    margin-top: 8px;
    margin-bottom: 20px;
}

.primary-btn,
.secondary-btn {
    width: max-content;
    padding: 10px 40px;
    cursor: pointer;
    background-color: var(--main-color);
    color: #fdfdfd;
    transition: all 0.3s;
    border: transparent;
    border-radius: 5px;
    font-family: inherit;
}

.primary-btn {
    width: 100%;
}

.primary-btn:hover,
.secondary-btn:hover {
    background-color: #4737a3;
}

.secondary-btn {
    border: 1px solid #fdfdfd;
}

.edit-dialog {
    border-radius: 10px;
    border: 2px solid var(--main-color);
    padding: 30px;
    background-color: #f8f6ff;
    width: 550px;
}
</style>
