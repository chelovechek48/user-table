<script>
export default {
  name: 'AppForm',
  props: {
    usernames: {
      type: Array,
      required: true,
    },
  },
};
</script>

<template>
  <form class="form" action="" method="get">
    <input
      class="form__item"
      type="text" name="name" id="name"
      placeholder="имя"
    >
    <input
      class="form__item"
      type="tel" name="phone" id="phone"
      placeholder="телефон"
    >
    <select
      class="form__item"
      name="parent" id="parent"
    >
      <option v-for="name in usernames" :key="name" :value="name">
        {{ name }}
      </option>
    </select>
    <button class="form__item">Сохранить</button>
  </form>
</template>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
.form__item {
  box-shadow: 0 0 0 2px gray;
}
</style>
