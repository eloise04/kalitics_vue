<template>
  <div>
    <input type="text" v-model="user.name" placeholder="Nom du responsable" />
    <VueDatePicker v-model="user.startedAt" placeholder="Date de début"/>
    <VueDatePicker v-model="user.endAt" placeholder="Date de fin"/>
    <button @click="saveUser">Enregistrer</button>
  </div>
</template>

<script>
import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'

export default {
  components: { VueDatePicker },
  props: {
    userData: {
      type: Object,
      default: () => ({})
    }
  },
  data() {
    return {
      user: { ...this.userData }
    };
  },
  methods: {
    saveUser() {
      this.$emit('save', this.user);
      this.user = {};
    }
  }
}
</script>
