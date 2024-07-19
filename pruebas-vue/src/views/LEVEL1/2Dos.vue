<template>
    <div>
        <h1> 2 - REF // REACTIVE // COMPUTED </h1>

        <h3>Counter con ref: {{ counterRef }} <button @click.prevent="incrementarRef"> + </button></h3>

        <h3>Counter con reactive: {{ state.counterReactive }} <button @click.prevent="incrementarReactive"> + </button></h3>

        <section style="display: flex; gap: 20px;">
            <input type="text" v-model="character">
            <button @click.prevent="guardarPalabras"> Add </button>
        </section>
        <p> {{ characterCount }} / 200 </p>
        <ul>
            <li v-for="(palabra, index) in reversedPalabras" :key="index">
                    {{ palabra }}
            </li>
        </ul>

    </div>
</template>


<script setup>

import { ref, reactive, computed } from 'vue';

// Ref
const counterRef = ref(10)

const incrementarRef = () => {
    counterRef.value++
}

// Reactive
const state = reactive({
    counterReactive: 100,
})

const incrementarReactive = () => {
    state.counterReactive++
}

                    // Computed
// EJEMPLO 1
// defino la variable que va a ser reactiva, en este caso lo q ponga el usuario por el input
const character = ref('')

//creo una varible characterCount que cuando la llame, se ejecuta un COMPUTED (es una funcion d vue) que cuando CAMBIE el valor de character, se ejecuta esta funcion y me retorna el lenth de la variable character
const characterCount = computed(() => {
    return character.value.length
})
//basicamente no modifico nada, solamente ejecuto una funcion sobre un valor reactivo, eso es computed


//EJEMPLO 2
const palabras = ref([])

const guardarPalabras = () => {
    palabras.value.push(character.value)
}

//ahora quiero AGREGAR UN COMPUTED para que me TRANSFORME Y MANIPULE EL arreglo REACTIVO de palabras
//quiero q me lo de vuelta y me muestre primero las ultimas

// SIEMPRE CAMBIE EL ARREGLO PALABRAS, se ejecuta este computed
const reversedPalabras = computed(() => {
    //podria hacer un
    // return palabras.value.reverse() Y FUNCIONA PERO ESTA MAL, pq 
    // no tengo que modificar el arreglo original, sino manipularlo

    //ENTONCES creo una copia y ahi si puedo manejarme
    // por eso uso el ... para crear una copia del arr original palabras
    return [...palabras.value].reverse();
});


</script>


<style lang="scss" scoped>
</style>