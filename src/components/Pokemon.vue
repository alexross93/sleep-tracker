<template>
  <div>
    <div v-if="pokemon" class="w-3/12 m-auto bg-purple-100 mt-16 shadow-2xl flex justify-center flex-col items-center">
      <h3 class="text-2xl text-green-900 uppercase">{{pokemon.name}}</h3>
	  <div class="flex justify-center">
		  <img class="w-48" :src="pokemon.sprites.front_shiny" alt="">
	  </div>
	  <h3 class="text-yellow-400"> Types</h3>
	  <div v-for="(type, index) in pokemon.types" :key="index">
		  <h5 class="text-blue-900">{{type.type.name}}</h5>
	  </div>
    </div>
  </div>
</template>

<script>
import { reactive, toRefs } from 'vue'
import { useRoute } from 'vue-router'

export default {
  name: 'Pokemon',
  components: {},

  setup () {
    const route = useRoute()

    const state = reactive({
      pokemon: null
    })

    fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}`)
      .then((res) => res.json())
      .then((data) => {
        state.pokemon = data
      })

    return { ...toRefs(state) }
  }
}

</script>