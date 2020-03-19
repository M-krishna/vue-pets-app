<template>
  <div class="home">
    {{ getAllPets }}
    <b-button class="btn btn-info" @click="togglePetForm">Add</b-button>
    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">

      <b-form-group id="input-group-2" label="Pet Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.name"
          required
          placeholder="Enter name"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Pet Age:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.age"
          required
          placeholder="Enter Age"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Species:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="form.species"
          :options="['cats', 'dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'Home',
  data () {
    return {
      form: {
        name: '',
        age: '',
        species: null
      },
      showPetForm: false
    }
  },
  computed: {
    ...mapGetters([
      'getAllPets'
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
      const { name, age, species } = this.form
      const payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)
    }
  }
}
</script>
