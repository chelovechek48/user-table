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
  <form class="form" action="">
    <input class="form__item" type="text" name="name" id="name" placeholder="имя">
    <input class="form__item" type="text" name="phone" id="phone" placeholder="телефон">
    <select class="form__item" name="parent" id="parent">
      <option v-for="user in users" :key="user.name" :value="user.name">
        {{ user.name }}
      </option>
    </select>
    <button class="form__item">Сохранить</button>
  </form>
</template>

<style scopep>
.form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
.form__item {
  box-shadow: 0 0 0 2px gray;
}
</style>
