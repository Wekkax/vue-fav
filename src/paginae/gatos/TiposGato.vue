<script setup lang="ts">
import { Card, CardContent } from '@/components/ui/card';
import { characters } from '@/paginae/simpsons/data';
import { computed, ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();

const inPagina = 6;

const nuncPagina = ref(1);

const totalPaginae = Math.ceil(characters.length / inPagina);

const listaSimpsons = computed(() => {
    const inicio = (nuncPagina.value - 1) * inPagina;
    const fin = inicio + inPagina;
    return characters.slice(inicio, fin);
});

const ireAdPaginam = (pagina: number) => {
    if (pagina >= 1 && pagina <= totalPaginae) {
        nuncPagina.value = pagina;
    }
};

const paginaMumeri: number[] = [...Array(totalPaginae)].map((_, i) => i + 1);
</script>

<template>
    <div class="fixed right-30 mt-10 z-50 text-white font-sans text-center flex flex-col justify-center">
        <Button asChild class="bg-[rgb(155,240,140)] py-3 px-5 text-base hover:bg-[rgb(240,148,147)] transition-all border border-white rounded-full shadow-lg">
        <RouterLink to="/gatos">Volver a la página anterior</RouterLink>
        </Button>
    </div>
    <div class="fixed right-8 mt-10 z-50 text-white font-sans text-center flex flex-col justify-center">
        <Button asChild class="bg-[rgb(155,240,140)] py-3 px-5 text-base hover:bg-[rgb(240,148,147)] transition-all border border-white rounded-full shadow-lg">
        <RouterLink to="/">Salir</RouterLink>
        </Button>
    </div>

<section class="bg-[rgb(237,114,112)] min-h-screen w-full flex flex-col items-center">
    <div class="flex flex-col items-center gap-x-8 justify-center w-full max-w-[1400px] my-8 mx-auto text-white">
        <div class="text-center">
            <h1 class="font-bold text-xl mb-5">Gatos en adopción</h1>
            <p class="mb-5">¡Echa un vistazo a nuestros gatos disponibles para adoptar!</p>
        </div>

        <div class="grid grid-cols-2 md:grid-cols-3 gap-8 mx-auto">
            <Card 
            class="cursor-pointer w-[220px] h-[240px] hover:bg-[rgb(155,240,140)] hover:text-white transition-colors border-4 border-white"
            >
            </Card>
        </div>
        
        <div class="flex items-center justify-center gap-2 mt-4">
        <button
            @click="ireAdPaginam(nuncPagina - 1)"
            :disabled="nuncPagina === 1"
            :class="[
                'px-4 py-2 rounded-md font-medium transition-colors',
                nuncPagina === 1
                ? 'bg-gray-200 text-gray-400 cursor-not-allowed'
                : 'bg-[rgb(155,240,140)] hover:bg-[rgb(243,188,187)] hover:text-white'
            ]"
        >
            Anterior
        </button>

        <button
            v-for="pagina in paginaMumeri"
            @click="ireAdPaginam(pagina)"
            :class="['w-10 h-10 rounded-md font-medium transition-colors',
            nuncPagina === pagina
            ? 'bg-[rgb(243,188,187)] text-white'
            : 'bg-[rgb(155,240,140)] hover:bg-[rgb(243,188,187)] hover:text-white'
            ]"
        >
            {{ pagina }}
        </button>

        <button
            @click="ireAdPaginam(nuncPagina + 1)"
            :disabled="nuncPagina === totalPaginae"
            :class="[
                'px-4 py-2 rounded-md font-medium transition-colors',
                nuncPagina === totalPaginae
                ? 'bg-gray-200 text-gray-400 cursor-not-allowed'
                : 'bg-[rgb(155,240,140)] hover:bg-[rgb(243,188,187)] hover:text-white'
            ]"
        >
            Siguiente
        </button>
        </div>

    </div>
</section>

</template>

<style scoped>

</style>