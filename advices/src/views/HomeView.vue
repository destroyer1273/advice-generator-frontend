<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
const advice = ref({});
const isLoading = ref(false);
const updateAdvice = async () => {
    try {
        isLoading.value = true;
        const response = await axios.get("https://api.adviceslip.com/advice");
        advice.value = response.data.slip;
        isLoading.value = false;
    } catch (error) {
        console.log("Ошибка: ", error);
    }
}
onMounted(async () => {
    await updateAdvice();
});
</script>

<template>
  <div class="container">
    <div class="center">
        <p class="center__p">ADVICE #{{ advice.id }}</p>
        <h3 class="center__h3">"{{ advice.advice }}"</h3>
        <div class="toResize">
            <svg class="center__img1" height="16" xmlns="http://www.w3.org/2000/svg"><g fill="none" fill-rule="evenodd"><path fill="#4F5D74" d="M0 8h196v1H0zM248 8h196v1H248z"/><g transform="translate(212)" fill="#CEE3E9"><rect width="6" height="16" rx="3"/><rect x="14" width="6" height="16" rx="3"/></g></g></svg>
        </div>
        
        <button class="center__btn" @click="updateAdvice" :disabled="isLoading">
            <svg class="center__img2" width="24" height="24" xmlns="http://www.w3.org/2000/svg"><path d="M20 0H4a4.005 4.005 0 0 0-4 4v16a4.005 4.005 0 0 0 4 4h16a4.005 4.005 0 0 0 4-4V4a4.005 4.005 0 0 0-4-4ZM7.5 18a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Z" fill="#202733"/></svg>
        </button>
    </div>
  </div>
</template>

<style scoped>
    .container {
        background-color: #111726;
        width: 100%;
        height: 100vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    .center {
        margin: 0 auto;
        width: 80vw;
        max-width: 527px;
        background-color: #31314d;
        border-radius: 10px;
        padding: 40px 21px 60px 21px;
        min-height: 306px;
        display: flex;
        flex-direction: column;
        align-items: center;
        position: relative;
        
    }

    .center__p {
        color: #00ed6f;
        font-weight: 600;
        text-align: center;
        font-size: 12px;
        letter-spacing: 4px;
        margin-bottom: 30px;
    }
    .center__h3 {
        text-align: center;
        color: #FFF;
        font-weight: 600;
        font-size: 25px;
        padding: 0 15px;
        margin-bottom: 20px;
    }
    .center__btn {
        position: absolute;
        bottom: -35px;
        background-color: #00ed6f;
        border: none;
        border-radius: 40px;
        padding: 20px;
        width: 64px;
        height: 64px;
        cursor: pointer;
        transition: box-shadow 0.3s ease-in-out;
    }
    /* .toResize {
        width: 80%;
        position: absolute;
        bottom: 50px;
        overflow: hidden;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .center__img1 {
        width: 100%;
    } */
    .toResize {
    width: 80%;
    position: absolute;
    bottom: 50px;
    left: 50%; /* центрируем контейнер */
    transform: translateX(-50%); /* точно по центру */
    overflow: hidden;
}

.center__img1 {
    position: relative;
    left: 50%; /* центрируем SVG внутри */
    transform: translateX(-50%);
    width: 444px; /* оригинальная ширина */
    height: 16px;
}
    .center__btn:hover {
        box-shadow: 0px 0px 17px 10px #00ed6f;
    }
</style>
