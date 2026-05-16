<script setup lang="ts">
import { Card, CardContent } from '@/components/ui/card';
import { computed, ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();

const gatosList = [
    { nombre: 'Bollo', foto: '93027c17-955e-4e52-8fbe-2f024b67e912_16-9-discover-aspect-ratio_default_0.jpg' },
    { nombre: 'Cruasán', foto: 'British_shorthair_Irina_AEA.JPG' },
    { nombre: 'Napolitana', foto: 'Benny-1.jpeg' },
    { nombre: 'Toña', foto: 'Cat_November_2010-1a.jpg' },
    { nombre: 'Galleta', foto: 'Como-educar-a-un-gato-agresivo-Blog-de-Pampermut.jpg' },
    { nombre: 'Panini', foto: 'Gatito-tumbado-min.jpg' },
    { nombre: 'Rollito', foto: 'GATO_UNAM-1024x768.jpg' },
    { nombre: 'Berlina', foto: 'GB09_348_Moway-4-1024x680.jpg' },
    { nombre: 'Pan', foto: 'colores-pelo-gato.jpg' },
    { nombre: 'Bizcocho', foto: 'cuales-son-las-razas-de-gatos-mas-populares-en-colombia.jpg' },
    { nombre: 'Magdalena', foto: 'fluffy-red-cat-resting-in-bright-sunlight-2022-08-01-02-05-31-utc-min.jpg' },
    { nombre: 'Sobao', foto: 'gato-bebe_c0649b04_230110201006_900x900.jpg' },
    { nombre: 'Coca', foto: 'gatos-pueden-comer-zanahoria.jpg' },
    { nombre: 'Ensaimada', foto: 'istockphoto-1443562748-612x612.jpg' },
    { nombre: 'Hojaldre', foto: 'poly.jpg' },
    { nombre: 'Empanadilla', foto: 'sitesdefaultfilesstylessquare_medium_440x440public2022-06Siamese201.jpg' },
    { nombre: 'Roscón', foto: 'TIMIDO.jpg' },
    { nombre: 'Donut', foto: 'Togor-recien-llegado-scaled.jpg' }
];

const inPagina = 6;

const nuncPagina = ref(1);

const totalPaginae = Math.ceil(gatosList.length / inPagina);

const listaGatos = computed(() => {
    const inicio = (nuncPagina.value - 1) * inPagina;
    const fin = inicio + inPagina;
    return gatosList.slice(inicio, fin);
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

        <div class="grid grid-cols-2 md:grid-cols-3 gap-8 mx-auto pt-8">
            <Card 
            v-for="gato in listaGatos" :key="gato.nombre"
            class="group cursor-pointer w-[220px] h-[240px] bg-white hover:bg-[rgb(155,240,140)] transition-colors border-4 border-white overflow-hidden flex flex-col"
            >
                <CardContent class="p-0 flex-1 overflow-hidden">
                    <img :src="`/imagines/gatos/gatoscard/${gato.foto}`" :alt="gato.nombre" class="w-full h-full object-cover" />
                </CardContent>
                <div class="h-10 shrink-0 flex items-center justify-center font-bold text-[#444] group-hover:text-white">
                    {{ gato.nombre }}
                </div>
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