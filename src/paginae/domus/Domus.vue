<script setup lang="ts">
import Button from '@/components/ui/button/Button.vue';

import {
  Dialog,
  DialogContent,
  DialogDescription,
  DialogHeader,
  DialogTitle,
  DialogTrigger,
} from '@/components/ui/dialog'
import { Input } from '@/components/ui/input'
import { ref } from 'vue';


import {
  Tooltip,
  TooltipContent,
  TooltipProvider,
  TooltipTrigger,
} from '@/components/ui/tooltip'

const dialogApertaEst = ref<boolean>(false)
const quaestio = ref<string>('')

</script>


<template>

<div class="bg-[rgb(158,89,163)] h-screen text-white font-sans text-center w-screen flex flex-col justify-center items-center gap-12 fixed overflow-hidden">

<img class="absolute opacity-20" src="/imagines/tonitrui.png" alt="">

  <h1 class="text-5xl md:text-7xl lg:text-8xl font-bold pb-5 md:pb-20 z-10 transition-all">
    <span class="text-[rgb(236,28,184)]">Diseño</span> Web y 
    <br>
    Apps <span class="text-[rgb(236,28,184)]">Interactivas</span>
  </h1>

  <p class="text-lg md:text-2xl transition-all">
    Aprendiendo a crear aplicaciones web
  </p>

  <div class="z-10">

      <Dialog
        :open="dialogApertaEst"
        @update:open="dialogApertaEst = $event"
      >

      <TooltipProvider>
      <Tooltip>
      <TooltipTrigger as-child>
        <DialogTrigger as-child>
          <Button class="bg-[rgb(155,240,140)] mr-2 md:py-5 md:px-6 md:text-lg hover:bg-[rgb(140,211,240,0.7)] transition-all">
            Sí o No
          </Button>
        </DialogTrigger>
      </TooltipTrigger>
      <TooltipContent>
        <p>Pregunta al oráculo</p>
      </TooltipContent>
      </Tooltip>
      </TooltipProvider>

        <DialogContent class="sm:max-w-[425px] bg-[rgb(21,25,52)] text-white border-[rgb(140,211,240)]">
          <DialogHeader>
            <DialogTitle class="text-white">Pregúntame</DialogTitle>
            <DialogDescription class="text-gray-300">
              No sigas con tus dudas, yo te responderé SÍ o NO
            </DialogDescription>
          </DialogHeader>

          <div class="mt-4">
            <Input
              class="bg-[rgb(31,35,62)] text-white placeholder:text-gray-400 border-[rgb(140,211,240)]"
              placeholder="Escribe tu pregunta aquí..."
              v-model="quaestio"
            />
          </div>

        </DialogContent>
    </Dialog>

    <TooltipProvider>
    <Tooltip>
    <TooltipTrigger as-child>
    <Button class="bg-[rgb(155,240,140)] mr-2 md:py-5 md:px-6 md:text-lg hover:bg-[rgb(140,211,240,0.7)] transition-all">
      <RouterLink to="/batman">Batman</RouterLink>
    </Button>
    </TooltipTrigger>
      <TooltipContent>
        <p>Aprender sobre Batman</p>
      </TooltipContent>
    </Tooltip>
    </TooltipProvider>

    <TooltipProvider>
    <Tooltip>
    <TooltipTrigger as-child>
    <Button class="bg-[rgb(155,240,140)] mr-2 md:py-5 md:px-6 md:text-lg hover:bg-[rgb(140,211,240,0.7)] transition-all">
      <RouterLink to="/simpsons">Simpsons</RouterLink>
    </Button>
    </TooltipTrigger>
      <TooltipContent>
        <p>Aprender sobre los Simpson</p>
      </TooltipContent>
    </Tooltip>
    </TooltipProvider>

    <TooltipProvider>
    <Tooltip>
    <TooltipTrigger as-child>
    <Button class="bg-[rgb(155,240,140)] mr-2 md:py-5 md:px-6 md:text-lg hover:bg-[rgb(140,211,240,0.7)] transition-all">
      <RouterLink to="/gatos">Gatos</RouterLink>
    </Button>
    </TooltipTrigger>
      <TooltipContent>
        <p>Aprender sobre gatos</p>
      </TooltipContent>
    </Tooltip>
    </TooltipProvider>
  </div>

</div>
  
</template>

<style scoped>


</style>

