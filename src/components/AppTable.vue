<script>
export default {
  name: 'AppTable',
  props: {
    usersTree: {
      type: Array,
      required: true,
    },
    isChild: {
      type: Boolean,
      required: false,
      default: true,
    },
  },
};
</script>

<template>
  <ul :class="isChild ? 'table__child-list' : 'table'">
    <li
      v-for="parentUser in usersTree" :key="parentUser.name"
      v-if="parentUser.children.length !== 0"
    >
      <details class="table__details">
        <summary class="table__summary">
          <div class="table__item table__item_has-child">
            <div class="table__cell">
              {{ parentUser.name }}
            </div>
            <div class="table__cell">
              {{ parentUser.phone }}
            </div>
          </div>
        </summary>
        <AppTable :users-tree="parentUser.children" />
      </details>
    </li>
    <li v-else class="table__item">
      <div class="table__cell">
        {{ parentUser.name }}
      </div>
      <div class="table__cell">
        {{ parentUser.phone }}
      </div>
    </li>
  </ul>
</template>

<style scoped>
.table {
  font-size: 1.25rem;
  width: 15em;
  padding: 0.25rem;
}

.table,
.table__child-list {
  margin-top: 0.25rem;
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  background-color: gray;
}

.table__child-list {
  margin-top: 0.25rem;
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.table__cell {
  flex: 1 1 50%;
}

.table__item {
  display: flex;
  padding: 0.25rem 0.5rem;
  padding-left: 2rem;
  background-color: rgb(192, 192, 192);
}

.table__item_has-child {
  position: relative;
}
.table__item_has-child:before,
.table__details:not([open]) .table__item_has-child:after {
  content: '';
  position: absolute;
  top: 50%;
  left: 1rem;
  transform: translate(-50%, -50%);
  background-color: #000;
}

.table__details .table__item_has-child:before {
  width: 0.8rem;
  height: 2px;
}
.table__details:not([open]) .table__item_has-child:after {
  width: 2px;
  height: 0.8rem;
}
.table__details .table__item_has-child {
  cursor: pointer;
}

.table__details[open] {
  z-index: 1;
  position: relative;

  border: 0.25rem solid #000;
  margin: -0.25rem;
}

.table__summary {
  list-style: none;
}
</style>
