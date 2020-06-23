<template>
  <div class="ui menu table__nav">
    <h1 class="table__nav-header">Инспекция по ресторанам</h1>
    <div class="right menu table__nav-right">
      <div class="button__wrapper">
        <button
          type="button"
          class="ui blue button"
          @click="colVisible = !colVisible"
        >
          Редактировать таблицу
        </button>
        <ul class="column__list">
          <li
            v-for="(col, i) in columns"
            :key="col.value"
            v-show="colVisible"
            :class="col.visible ? 'bg--green' : 'bg--red'"
            @click="updateVisible(i)"
            class="column__list-item"
          >
            {{ col.description }}
          </li>
        </ul>
      </div>
      <div class="date__wrapper">
        <div class="ui input date__item">
          <input type="date" :value="date.from" @change="changeDate($event,'from')" />
        </div>
        <div class="ui input">
          <input type="date" :value="date.to" @change="changeDate($event,'to')"/>
        </div>
      </div>
      <div class="table__search">
        <div class="ui checkbox search__checkbox">
          <input type="checkbox" @change="check" v-model="checked" />
          <label>Искать по всем полям</label>
        </div>
        <div class="ui icon input align-self-center">
          <input
            type="text"
            placeholder="Поиск..."
            @input="updateSearch($event)"
          />
          <i class="search icon"></i>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    columns: Array,
    date: Object
  },
  data() {
    return {
      checked: false,
      colVisible: false,
    };
  },
  methods: {
    updateVisible(index) {
      this.$emit("update:colVisible", index);
    },

    updateSearch(e) {
      this.$emit("update:search", e.target.value);
    },
    check() {
      this.$emit("update:checkbox", this.checked);
    },
    changeDate(e, key) {
      this.$emit('update:date',e.target.value,key);
    }
  },
};
</script>

<style>
.table__nav {
  align-items: flex-end;
  padding: 5px 10px;
}
.table__nav-header {
  margin: 0;
}
.table__nav-right {
  align-items: flex-end;
}
.table__search {
  display: flex;
  flex-direction: column;
}
.button__wrapper {
  position: relative;
}
.column__list {
  position: absolute;
  top: 100;
  left: 0;
  width: 100%;
  list-style: none;
  margin: 0;
  padding: 0;
}
.column__list-item {
  padding: 5px 10px;
  border: 0.5px solid black;
  cursor: pointer;
}
.search__checkbox {
  margin-bottom: 5px;
}
.date__wrapper {
  margin: 0 10px;
}
.date__item {
  margin-right: 5px;
}
</style>
