<template>
    <button @click="showCreateForm = true">Ajouter un utilisateur</button>
    <UserForm v-if="showCreateForm" @save="addUser" />

    <div v-for="user in users" :key="user.id">
        <span>{{ user.name }}</span>
        <span>{{ formatDate(user.startedAt) }}</span>
        <span>{{ formatDate(user.endAt) }}</span>
        <button @click="editUser(user)">Modifier</button>
        <button @click="deleteUser(user.id)">Supprimer</button>
    </div>
</template>
  
<script>
import UserForm from './UserForm.vue';

export default {
    components: { UserForm },
    data() {
        return {
            users: [],
            currentUser: null,
            showCreateForm: false,
        };
    },
    mounted() {
        fetch('/data.json')
            .then(response => response.json())
            .then(data => {
                this.users = data;
            })
            .catch(error => console.error('Error loading data:', error));
    },
    methods: {
        formatDate(dateString) {
            const options = { year: 'numeric', month: '2-digit', day: '2-digit' };
            return new Date(dateString).toLocaleDateString('fr-FR', options);
        },
        addUser(user) {
            if (this.currentUser) {
                const index = this.users.findIndex(u => u.id === this.currentUser.id);
                if (index !== -1) {
                    this.users.splice(index, 1, { ...user, id: this.currentUser.id });
                }
            } else {
                this.users.push({ ...user, id: this.users.length + 1 });
            }
            this.showCreateForm = false;
            this.currentUser = null;
        },
        editUser(user) {
            this.currentUser = { ...user };
            this.showCreateForm = true;
        },
        deleteUser(userId) {
            this.users = this.users.filter(user => user.id !== userId);
        },
    },
}
</script>
  