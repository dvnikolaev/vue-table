<template>
  <table class="ui selectable celled table">
    <TableHead
      :columns="columns"
      @sort:list="sortKey"
      @update:search="updateSearch"
    />
    <TableBody :list="filteredList" :columns="columns" />
  </table>
</template>

<script>
import TableHead from "./TableParts/TableHead";
import TableBody from "./TableParts/TableBody";

export default {
  props: {
    columns: Array,
    list: Array,
    search: String,
    checked: Boolean,
    date: Object
  },
  data() {
    return {
      sortBy: "",
      reverse: false,
    };
  },
  methods: {
    sortKey(value) {
      if (this.sortBy !== value) {
        this.sortBy = value;
        this.reverse = true;
        return this.list.sort((a, b) => {
          return a[value].toLowerCase().localeCompare(b[value].toLowerCase());
        });
      } else {
        this.sortBy = value;

        if (this.reverse) {
          this.reverse = !this.reverse;
          return this.list.sort((a, b) => {
            return b[value].toLowerCase().localeCompare(a[value].toLowerCase());
          });
        } else {
          this.reverse = !this.reverse;
          return this.list.sort((a, b) => {
            return a[value].toLowerCase().localeCompare(b[value].toLowerCase());
          });
        }
      }
    },
    updateSearch(value) {
      this.search = value;
    },
  },
  computed: {
    filteredList() {
      return this.list.filter((item) => {
        return this.columns.some((elem) => {
          const searchAllFields = this.checked
            ? true
            : elem.visible
            ? true
            : false;

          return (
            item[elem.value]
              .toLowerCase()
              .trim()
              .indexOf(this.search.toLowerCase().trim()) > -1 && searchAllFields &&
              (item.inspection_date >= this.date.from && item.inspection_date <= this.date.to)
          );
        });
      });
    },
  },
  components: {
    TableHead,
    TableBody,
  },
};
</script>
