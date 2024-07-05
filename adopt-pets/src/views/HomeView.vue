<template>
  <div class="home">
    <h1>Adopt a new best friend</h1>
    <h3>Total Pets available: {{ animalsCount }}</h3>
    <button class="btn btn-primary" @click="togglePetForm" >Add New Pet</button>
    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
      <b-form-group id="input-group-2" label="Pet's Name:" label-for="input-2" class="mt-4">
        <b-form-input
          id="input-2"
          v-model="formData.name"
          placeholder="Enter name"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Species:" label-for="input-3" class="mt-4">
        <b-form-select
          id="input-3"
          v-model="formData.species"
          :options="['cat', 'dog']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-4" label="Pet's Age:" label-for="input-4" class="mt-4">
        <b-form-input
          id="input-4"
          type="number"
          v-model="formData.age"
          placeholder="Enter age"
          required
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="success" class="mt-4">Submit</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'HomeView',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        species: null
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats'
    ])
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, age, name } = this.formData

      const payload = {
        pet: {
          name,
          species,
          age
        }
      }

      this.addPet(payload)

      this.formData = {
        name: '',
        age: 0,
        species: null
      }
    }
  }
}
</script>
