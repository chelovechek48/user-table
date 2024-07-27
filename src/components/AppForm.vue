<script>
export default {
  name: 'AppForm',
  props: {
    usernames: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      formData: {
        name: null,
        phone: null,
        parent: false,
      },
    };
  },
};
</script>

<template>
  <form class="form" action="" method="get" @submit.prevent="$emit('addUser', formData)">
    <input
      class="form__item"
      type="text" name="name" id="name"
      placeholder="имя"
      required
      v-model="formData.name"
    >
    <input
      class="form__item"
      type="tel" name="phone" id="phone"
      placeholder="телефон"
      required
      v-model="formData.phone"
    >
    <select
      class="form__item"
      name="parent" id="parent"
      v-model="formData.parent"
    >
      <option :value="false">
        Без начальника
      </option>
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
  border: 0.25rem solid gray;
  font-size: 1.25rem;
  padding: 0.25rem 0.5rem;
}
</style>
