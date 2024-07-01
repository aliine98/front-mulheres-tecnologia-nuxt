<template>
    <section class="form-section">
        <form class="add-woman-form" @submit.prevent="addWoman(name, image, desc)">
            <h2 class="form-title">Adicionar nova mulher</h2>
            <label>Nome: <input type="text" v-model="name" class="form-input" required /></label>
            <label>Url da imagem: <input type="text" v-model="image" class="form-input" required /></label>
            <label>Descrição: <textarea v-model="desc" class="form-input" rows="5" required></textarea></label>
            <button type="submit" class="primary-btn">Adicionar</button>
        </form>
        <dialog ref="dialog" class="complete-dialog">
            <div class="dialog-content">
                <p>Mulher cadastrada com sucesso!</p>
                <img src="../assets/verify.png" class="dialog-icon" alt="" />
                <button @click="closeDialog" class="primary-btn">Fechar</button>
            </div>
        </dialog>
    </section>
</template>
<script setup lang="ts">
import { ref } from 'vue';
import { reloadNuxtApp } from 'nuxt/app';
import type { Woman } from '../model/Woman';

const name = ref('');
const image = ref('');
const desc = ref('');
const dialog = ref(null);

function closeDialog() {
    dialog.value!.close();
    reloadNuxtApp();
}

async function addWoman(name: string, image: string, desc: string) {
    const woman: Woman = { name, image, desc };
    await $fetch('https://backend-teste-vn7a.onrender.com/nova-mulher', { method: 'POST', body: woman });
    dialog.value!.showModal();
}
</script>
<style scoped>
.form-section {
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem;
}

.add-woman-form {
    display: grid;
    gap: 2rem;
}

.form-title {
    color: var(--main-color);
    font-size: 1.8rem;
}

.form-input {
    display: block;
    border-radius: 10px;
    border: 2px solid var(--main-color);
    width: 100%;
    padding: 8px;
    margin-top: 10px;
}

.primary-btn {
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

.primary-btn:hover {
    background-color: #4737a3;
}

.complete-dialog {
    font-size: 1.3rem;
    border-radius: 10px;
    border: 2px solid var(--main-color);
    padding: 50px 30px 20px;
    text-align: center;
    background-color: #f8f6ff;
}

.dialog-content {
    display: grid;
    place-items: center;
}

.dialog-icon {
    margin-bottom: 2rem;
    width: 70px;
}
</style>
