<template>
    <div>
        <div v-if="!pokemon.habilidades">
            Selecione um Pokémon
        </div>
        <div v-else>
            <table class="table text-white">
                <tbody>
                    <transition-group name="lista">
                        <tr v-for="(h, indice) in pokemon.habilidades" :key="h"><!-- aqui o :key= antes tinha o valor "indice", porém ao animar grupos de elementos o javascript se perde na remoção de elementos e aninmação fica indiondizente com a realidade, então setamos a key como a habilidade, para apos a reorganizacao de elementos no array, ele conseguir remover o elemento certo, usando a descricao da habilidade que é exclusiva, como indice-->
                            <td>{{ h }}</td>
                            <td class="d-flex justify-content-end">
                                <button 
                                    type="button" 
                                    class="btn btn-danger btn-sm"
                                    @click="$emit('removerHabilidade', indice)"
                                >
                                    x
                                </button>
                            </td>
                        </tr>
                    </transition-group>
                </tbody>
            </table>
            <input 
                type="text"
                class="form-control" 
                placeholder="Adicionar habilidade"
                v-model="habilidade"
                @keyup.enter="adicionarHabilidade"
            >
        </div>
    </div>
</template>

<style scoped>
.table td {
    border: none;
}
</style>

<script>
export default {
   name: 'Habilidades',
   props: {
       pokemon: Object
   },
   data: () => ({
      habilidade: ''
   }),
   methods: {
       adicionarHabilidade() {
           this.$emit('adicionarHabilidade', this.habilidade);
           this.habilidade = '';
       }
   }
}
</script>