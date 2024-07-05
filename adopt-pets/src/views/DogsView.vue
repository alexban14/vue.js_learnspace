<template>
  <div>
    <h1>Dogs for Adoption</h1>
    <b-table striped hover :items="getAllDogs">
      <template #cell(name)="data">
        <router-link :to="`/pets/dogs/${data.index}`">
          {{ data.value }}
        </router-link>
      </template>
    </b-table>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'DogsView',
  data () {
    return {
    }
  },
  computed: {
    ...mapGetters([
      'getAllDogs'
    ])
  }
}
</script>
