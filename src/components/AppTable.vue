<script>
import usersList from '@/assets/json/usersInfo.json';

export default {
  data() {
    return {
      users: usersList,
    };
  },
};
</script>

<template>
  <ul class="table">
    <li class="table__item">
      <div class="table__cell">Имя</div>
      <div class="table__cell">Телефон</div>
    </li>
    <li class="table__item"
      v-for="user in users" :key="user.name">
      <div class="table__cell">{{ user.name }}</div>
      <div class="table__cell">{{ user.phone }}</div>
    </li>
  </ul>
</template>

<style scoped>
.table {
  width: 30rem;

  display: flex;
  flex-direction: column;
  gap: 2px;
}
.table__item {
  display: flex;
  gap: 2px;
}
.table__cell {
  flex: 0 0 50%;
  box-shadow: 0 0 0 2px gray;
}
</style>
