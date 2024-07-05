<template>
  <div>
    <h1>Cats for Adoption</h1>
    <b-table striped hover :items="getAllCats">
      <template #cell(name)="data">
        <router-link :to="`/pets/cats/${data.index}`">
          {{ data.value }}
        </router-link>
      </template>
    </b-table>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  data () {
    return {
    }
  },
  computed: {
    // ...mapState([
    //   'cats'
    // ])
    ...mapGetters([
      'getAllCats'
    ])
  }
}
</script>
