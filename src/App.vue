<script>
import AppTable from '@/components/AppTable';
import AppForm from '@/components/AppForm';

export default {
  name: 'App',
  components: {
    AppTable,
    AppForm,
  },
};
</script>

<template>
  <div class="container">
    <AppTable/>
    <AppForm/>
  </div>
</template>

<style>
@import 'styles/normalize.css';

.container {
  padding: 1rem;

  display: flex;
  gap: 2rem;
}
</style>
