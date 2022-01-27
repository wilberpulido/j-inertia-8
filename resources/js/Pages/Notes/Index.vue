<template>
    <app-layout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Modulo de notas
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="md:grid md:grid-cols-3 md:gap-6">
                    <div class="md:col-span-1">
                        <div class="px-4 sm:px-0">
                            <h3 class="text-lg text-gray-900">Listado de notas</h3>    
                            <p class="text-sm text-gray-600">
                                tomar el registro correcto y ejecutar cosas
                            </p>
                        </div>
                    </div>
                    <div class="md:col-span-2 mt-5 md:mt-0">
                        <div class="shadow bag-white md:rounded-md p-4">
                            <div class="flex justify-between">
                                <input 
                                    type="text" class="form-input rounded-md shadow-sm" placeholder="Buscar..." 
                                    v-model="q"
                                >
                                <Link class="bg-blue-500 hover:bg-blue-800 py-2 px-4 rounded-md text-white" :href="route('notes.create')">
                                    Crear nota
                                </Link>
                            </div>
                            <hr class="my-6">
                            <table>
                                <tr v-for="note in notes" >
                                    <td class="border px-4 py-2">
                                        {{ note.excerpt }}
                                    </td>
                                    <td class="px-4 py-2">
                                        <Link :href="route('notes.show',note.id)">Ver</Link>
                                    </td>
                                    <td class="px-4 py-2">
                                        <Link :href="route('notes.edit',note.id)">Edit</Link>
                                    </td>
                                </tr>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </app-layout>
</template>

<script>
    import { defineComponent } from 'vue'
    import AppLayout from '@/Layouts/AppLayout.vue'
        import { Link } from '@inertiajs/inertia-vue3';

    export default defineComponent({
        components: {
            AppLayout,
            Link,
        },
        props: {
            notes: Array,
        },
        data () {
            return {
                q:'',
            }
        },
        watch: {
            q: function (value) {
                this.$inertia.replace(this.route('notes.index',{q:value}))
            }
        },
    })
</script>
