<script>
import AppTable from '@/components/AppTable';
import AppForm from '@/components/AppForm';

import usersListDefault from '@/assets/json/usersList.json';

export default {
  name: 'App',
  components: {
    AppTable,
    AppForm,
  },

  data() {
    return {
      usersList: [],
      usersTree: [],
    };
  },
  computed: {
    usernames() {
      return this.usersList.map(user => user.name);
    },
  },
  methods: {
    getUsersList() {
      const localUsersList = localStorage.getItem('users-list');
      if (localUsersList) {
        return JSON.parse(localUsersList);
      }
      localStorage.setItem('users-list', JSON.stringify(usersListDefault));
      return usersListDefault;
    },
    getUsersThree() {
      const result = [];
      const users = {};

      this.usersList.forEach((item) => {
        const { ...properties } = item;
        users[item.name] = {
          ...properties,
          children: [],
        };
      });

      this.usersList.forEach((item) => {
        const user = users[item.name];
        if (item.parent) {
          users[item.parent].children.push(user);
        } else {
          result.push(user);
        }
      });
      return result;
    },
    updateData() {
      this.usersList = this.getUsersList();
      this.usersTree = this.getUsersThree();
    },
    addUserToStorage(userData) {
      const usersList = this.usersList;
      const { name } = userData;

      const temp = usersList.find(user => (user.name === name));
      if (!temp) {
        usersList.push(userData);
        localStorage.setItem('users-list', JSON.stringify(usersList));
        this.updateData();
      }
    },
  },

  mounted() {
    this.updateData();
  },
};
</script>

<template>
  <div class="container">
    <AppTable :users-tree="usersTree" :is-child="false" />
    <AppForm :usernames="usernames" @addUser="addUserToStorage($event)" />
  </div>
</template>

<style>
@import 'styles/normalize.css';

.container {
  padding: 1rem;

  display: flex;
  align-items: flex-start;
  gap: 2rem;
}
</style>
