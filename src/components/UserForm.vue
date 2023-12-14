<template>
  <div>
    <input type="text" v-model="user.name" placeholder="Nom du responsable" />
    <VueDatePicker v-model="user.startedAt" placeholder="Date de début" />
    <VueDatePicker v-model="user.endAt" placeholder="Date de fin" />
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
<style>
input[type=text],
select {
  width: 100%;
  padding: 12px 20px;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

input {
  margin-bottom: 5px;
}

button {
  width: 180px;
  background-color: #4CAF50;
  color: white;
  padding: 10px 14px;
  margin: 8px 5px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

span {
  margin: 8px 10px;
}

button:hover {
  background-color: #45a049;
}

div {
  border-radius: 5px;
}</style>