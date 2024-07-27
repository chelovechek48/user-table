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
  <ul :class="isChild ? '' : 'table'">
    <li
      v-for="parentUser in usersTree" :key="parentUser.name"
      v-if="parentUser.children.length !== 0"
    >
      <details class="table__details">
        <summary class="table__summary">
          <div class="table__item table__item_has-child_true">
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
    <li v-else class="table__item table__item_has-child_false">
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
  width: 12em;
}
.table__item {
  display: flex;
  padding: 0.25rem 0.5rem;
  padding-left: 1.5rem;
  gap: 0.5rem;
}
.table__cell {
  flex: 1 1 50%;
}

.table__item_has-child_false {
  background-color: rgb(192, 192, 192);
}
.table__item_has-child_true {
  background-color: rgb(160, 160, 160);
}
.table__item_has-child_true {
  position: relative;
}
.table__item_has-child_true:before {
  position: absolute;
  top: 0;
  left: 0;
}

.table__details[open] .table__item_has-child_true:before {
  content: '-';
}
.table__details:not([open]) .table__item_has-child_true:before {
  content: '+';
}


.table__summary {
  list-style: none;
}
</style>
