<!-- Los componentes siempre deben comenzar con letra mayúscula -->
<template> 
  <section>

      <div class="characters">

          <div class="characters__item" v-for="character in characters" :key="character.id">
          <CardCharacter :character="character" />
          </div>

      </div>   

  </section>
</template>
<script>

import { onMounted, computed } from 'vue' //usar solo vue
import { useStore } from 'vuex' //para usar store

import CardCharacter from '@/components/CardCharacter.vue'
import ListCharacters from '@/components/ListCharacters.vue';

export default {
  components: { CardCharacter },
    setup() {
        const store = useStore()
        const characters = computed(() => {
            return store.state.charactersFilter

        }
        )
        onMounted(() => {
            store.dispatch('getCharacters')
        }
        )

        return {
            characters
        }
    }
}
</script>

<style>
.characters {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 3rem;
    margin: 3rem 0;
}
</style>