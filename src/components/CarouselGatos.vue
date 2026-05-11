<script setup lang="ts">
import { Card, CardContent } from '@/components/ui/card'
import {
  Carousel,
  CarouselContent,
  CarouselItem,
  CarouselNext,
  CarouselPrevious,
} from '@/components/ui/carousel'
import Autoplay from 'embla-carousel-autoplay'

interface Props {
  photos: string[]
  basePath: string
  autoplayDelay?: number
  loop?: boolean
  dragFree?: boolean
}

const props = withDefaults (defineProps<Props>(), {
    autoplayDelay: 2000,
    loop: true,
    dragFree: true
})

</script>

<template>
<Carousel 
    class="w-full max-w-sm md:max-w-lg mx-auto"
    :opts="{
      loop: props.loop,
      dragFree: props.dragFree
    }"
    :plugins="[Autoplay({
      delay: props.autoplayDelay,
    })]"
    >
    <CarouselContent>
      <CarouselItem v-for="(fotos, index) in props.photos" :key="index">
        <div class="p-1">
          <Card class=" ">
            <CardContent class="flex aspect-[4/3] items-center justify-center p-3">
              
              <img 
                :src="`${ props.basePath }/${ fotos }.jpg`" 
                :alt="`Imagen ${ fotos } de Gatos`"
                class="w-full h-auto object-contain rounded-lg shadow-md"
                >

            </CardContent>
          </Card>
        </div>
      </CarouselItem>
    </CarouselContent>

    <CarouselPrevious class="text-[rgb(237,114,112)] hidden md:flex justify-center items-center hover:cursor-pointer hover:text-[rgb(155,240,140)] transition-colors" />
    <CarouselNext class="text-[rgb(237,114,112)] hidden md:flex justify-center items-center hover:cursor-pointer hover:text-[rgb(155,240,140)] transition-colors" />

  </Carousel>
</template>