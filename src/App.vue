<script setup>
import { onMounted, ref } from "vue";

let dataFilm = ref('')

// const data =   async () => {
//     try {
//         const response = await fetch("https://whenisthenextmcufilm.com/api");
//         if (!response.ok) {
//             throw new Error("Network response was not ok");
//         }
//         const data = await response.json();
//         dataFilm.value = data; // Asigna la URL a la variable reactiva
//     } catch (error) {
//         console.error("Hubo un problema con la petición Fetch:", error);
//     }
// };

const data = () => {
    fetch("https://whenisthenextmcufilm.com/api")
        .then(response => {
            if (!response.ok) {
                throw new Error("Network response was not ok");
            }
            return response.json(); // Devuelve la promesa de los datos JSON
        })
        .then(data => {
            dataFilm.value = data; // Asigna los datos a la variable reactiva
        })
        .catch(error => {
            console.error("Hubo un problema con la petición Fetch:", error);
        });
};

onMounted(data);

</script>

<template>
    <section>
        <img :src="dataFilm.poster_url" width="300" alt="" v-if="dataFilm.title" />
        <p v-else>Cargando...</p>
    </section>
</template>

<style scoped>
.logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
}

.logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
    filter: drop-shadow(0 0 2em #42b883aa);
}
</style>

<!-- <div>
<a href="https://vitejs.dev" target="_blank">
  <img src="/vite.svg" class="logo" alt="Vite logo" />
</a>
<a href="https://vuejs.org/" target="_blank">
  <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
</a>
</div> -->
<!-- <HelloWorld msg="Vite + Vue" /> -->
