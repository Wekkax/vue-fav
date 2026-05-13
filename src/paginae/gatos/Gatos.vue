<script setup lang="ts">
import Button from '@/components/ui/button/Button.vue'
import CarouselGatos from '@/components/CarouselGatos.vue'
import { ref } from 'vue';
import { Loader2, LucideBadgeCheck } from 'lucide-vue-next';
import { toast } from 'vue-sonner';
import type { DateValue } from 'reka-ui';
import { Label } from '@/components/ui/label'
import { Input } from '@/components/ui/input'
import { Calendar } from '@/components/ui/calendar'
import {
  Select,
  SelectContent,
  SelectGroup,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from '@/components/ui/select'
import {
  Popover,
  PopoverContent,
  PopoverTrigger,
} from '@/components/ui/popover'

const fotos = ["gato_adopcion1", "gato_adopcion2", "gato_adopcion3", "gato_adopcion6", "gato_adopcion7", "gato_adopcion8"];

const dia = ref<DateValue>()
const nombre = ref<string>('')
const apellido = ref<string>('')
const cita = ref<string>('')

const Cargando = ref<boolean>(false)

const mittereSubmit = async() => {

  Cargando.value = true

  toast(`¡Tu cita ha sido registrada con éxito!
  - Nombre: ${nombre.value} ${apellido.value}
  - Cita: ${cita.value || 'No especificada'}
  - Fecha: ${dia.value ? `${dia.value.day}/${dia.value.month}/${dia.value.year}` : 'No especificada'}`, {
    duration: 4000,
    position: 'top-center',
    icon: LucideBadgeCheck,
    style: {
      background: "#fff",
      color: "#ed7270",
      whiteSpace: 'pre-line',
    }
  }
)

 await new Promise(resolve => setTimeout(resolve, 2000))

  Cargando.value = false

  nombre.value = ''
  apellido.value = ''
  cita.value = ''
  dia.value = undefined
}
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

    <div class="flex flex-col lg:flex-row gap-8 items-center mb-10">
            <div class="hidden lg:block w-full lg:w-1/2 rounded-lg overflow-hidden shadow-lg">
              <div class="aspect-square">

                <iframe
                  src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d49289.495392383884!2d-0.4161537001176022!3d39.45591972765885!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0xd604fa239dc1353%3A0xbd1e32236eefe5c2!2sLa%20F%C3%A1brica%20de%20Huellas!5e0!3m2!1ses!2ses!4v1778670364377!5m2!1ses!2ses"
                  width="600" height="450" style="border:0;" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
              </div>
            </div>


            <div class="w-full max-w-md mx-auto lg:max-w-none lg:w-1/2 ">
              <form class="space-y-6 bg-white p-8 rounded-lg shadow-lg aspect-square"
                @submit.prevent="mittereSubmit"
              >
                <div class="space-y-2">

                  <Label for="nomen">Nombre</Label>
                  <Input id="nomen" v-model="nombre" required/>
                </div>

                <div class="space-y-2">

                  <Label for="cognomen">Apellidos</Label>
                  <Input id="cognomen" v-model="apellido" required/>

                </div>

                <div class="space-y-2">

                  <Label for="cita">Tipo de cita</Label>
                  <Select required v-model="cita">
                    <SelectTrigger class="border-gray-200 bg-white text-gray-900">
                      <SelectValue placeholder="Selecciona un tipo de cita" />
                    </SelectTrigger>
                    <SelectContent>
                      <SelectGroup>
                        <SelectItem value="Consulta">
                          Consulta
                        </SelectItem>
                        <SelectItem value="Adopción">
                          Adopción
                        </SelectItem>
                        <SelectItem value="Voluntariado">
                          Voluntariado
                        </SelectItem>
                        <SelectItem value="Otros">
                          Otros
                        </SelectItem>
                      </SelectGroup>
                    </SelectContent>
                  </Select>

                </div>

                <div class="space-y-2">

                  <Label>Fecha de la misión</Label>

                  <Popover>
                    <PopoverTrigger asChild>
                      <Button variant="outline">
                        <span v-if="dia">
                          {{dia.day}}/{{ dia.month }}/{{ dia.year }}
                        </span>
                        <span v-else class="text-gray-500">
                          Selecciona una fecha
                        </span>
                      </Button>
                    </PopoverTrigger>
                    <PopoverContent class="w-80">
                      <Calendar v-model="dia"/>

                    </PopoverContent>
                  </Popover>
                </div>

                <Button
                type="submit"
                class="w-full bg-[rgb(240,148,147)] hover:bg-[rgb(155,240,140)] text-white text-md mt-4"
                :disabled="Cargando"
                >
                  <Loader2 v-if="Cargando" class="animate-spin h-4 w-4 mr-2"/>
                  <span v-if="Cargando">Enviando...</span>
                  <span v-else>Pedir cita</span>
                </Button>

              </form>
            </div>
          </div>
          </div>
</template>


<style scoped>

</style>