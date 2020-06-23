<template>
  <thead>
    <tr>
      <th
        v-for="col in columns"
        :key="col.value"
        @click="sortBy(col.value)"
        v-show="col.visible"
      >
        {{ col.description }}
        <i class="arrows alternate vertical icon"></i>
      </th>
    </tr>
  </thead>
</template>

<script>
export default {
  props: {
    columns: Array,
  },
  methods: {
    sortBy(value) {
      this.$emit("sort:list", value);
    },
  },
};
</script>

<style>
.table__header {
  display: inline-block;
}
</style>
