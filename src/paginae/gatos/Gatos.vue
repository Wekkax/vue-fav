<script setup lang="ts">
import Button from '@/components/ui/button/Button.vue'
import CarouselGatos from '@/components/CarouselGatos.vue'

const fotos = ["gato_adopcion1", "gato_adopcion2", "gato_adopcion3", "gato_adopcion6", "gato_adopcion7", "gato_adopcion8"];
</script>

<template>
<div class="bg-[rgb(237,114,112)] min-h-screen w-full flex flex-col items-center">

    <div class="fixed bottom-4 left-1/2 transform -translate-x-1/2 z-50 text-white font-sans text-center flex flex-col justify-center">
        <Button asChild class="bg-[rgb(155,240,140)] py-3 px-5 text-base hover:bg-[rgb(240,148,147)] transition-all border border-white rounded-full shadow-lg">
        <RouterLink to="/">Salir</RouterLink>
        </Button>
    </div>

    <section class="relative w-full min-h-[40vh] text-white text-shadow-md text-shadow-[rgb(128,47,44)] font-sans text-center flex flex-col justify-center bg-cover bg-center bg-no-repeat" style="background-image: url('/imagines/gatos/fondo.jpg');">
        <img src="/imagines/gatos/deco1.png" alt="Decoración de Gatos" class="absolute top-16 left-10 w-40 h-auto">
        <img src="/imagines/gatos/deco2.png" alt="Decoración de Gatos" class="absolute top-16 right-10 w-36 h-auto">
        <h1 class="text-3xl font-bold mt-8 mb-2">¡Adopta un gato!</h1>
        <p>Descubre tu nuevo mejor amigo de 4 patas</p>
        
        <div class="mt-6">
            <Button asChild variant="default" class="bg-[rgb(155,240,140)] shadow-none mr-2 md:py-5 md:px-6 md:text-lg hover:bg-[rgb(240,148,147)] transition-all border-3 border-white rounded-full">
            <RouterLink to="/gatos/tipos" style="text-shadow: none; padding: 20px;">Gatos en adopción en nuestro refugio</RouterLink>
            </Button>
        </div>
    </section>

    <section class=" text-white font-sans text-center flex flex-col justify-center">
        <h2 class="text-2xl font-bold mt-10 mb-5">Algunos de nuestros peludos que ya han conseguido un hogar:</h2>
        <div>
            <CarouselGatos basePath="/imagines/gatos" :photos="fotos" :autoplay-delay="3000"/>
        </div>
    </section>

    <section class=" text-white font-sans text-center flex flex-col justify-center mb-10">
        <h2 class="text-2xl font-bold mt-10 mb-5">¿Por qué adoptar un gato?</h2>
        <p class="ml-30 mr-30 justify-around">Adoptar un gato no solo le brinda un hogar amoroso a un animal necesitado, sino que también puede mejorar tu vida de muchas maneras. Los gatos son compañeros leales, ofrecen compañía y pueden reducir el estrés. Además, al adoptar, estás ayudando a reducir la sobrepoblación de animales y apoyando a los refugios locales. Contacta con nosotros a través de este formulario para agenciar una visita y conocer a nuestros adorables gatos en persona. ¡Estamos aquí para ayudarte a encontrar el compañero perfecto para ti!</p>
    </section>

    <section>
            
    </section>
    
</div>
</template>


<style scoped>

</style>