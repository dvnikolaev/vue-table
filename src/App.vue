<template>
  <div id="app ui container">
    <TheNav
      :columns="columns"
      :date="date"
      @update:search="updateSearch"
      @update:colVisible="colVisible"
      @update:checkbox="updatecheckbox"
      @update:date="updateDate"
    />
    <TheTable
      :columns="columns"
      :list="list"
      :search="search"
      :checked="checked"
      :date="date"
    />
  </div>
</template>

<script>
import TheTable from "./components/TheTable";
import TheNav from "./components/TheNav";

export default {
  data() {
    return {
      columns: [
        {
          value: "business_name",
          description: "Наименование организации",
          visible: true,
        },
        {
          value: "business_address",
          description: "Адрес организации",
          visible: true,
        },
        {
          value: "business_city",
          description: "Город организации",
          visible: true,
        },
        {
          value: "business_phone_number",
          description: "Номер организации",
          visible: true,
        },
        {
          value: "inspection_date",
          description: "Дата инспекции",
          visible: true,
        },
        {
          value: "inspection_description",
          description: "Статус инспекции",
          visible: true,
        },
        {
          value: "inspection_type",
          description: "Тип проведения инспекции",
          visible: true,
        },
      ],
      list: [],
      search: "",
      checked: false,
      date: {
        from: '',
        to: ''
      }
    };
  },
  components: {
    TheTable,
    TheNav,
  },
  methods: {
    updateSearch(value) {
      this.search = value;
    },
    colVisible(index) {
      this.columns[index].visible = !this.columns[index].visible;
    },
    updatecheckbox(value) {
      this.checked = value;
    },
    updateDate(value, key) {
      this.date[key] = value;
    }
  },
  created() {
    fetch("/static/json.json")
      .then((response) => response.json())
      .then((data) => {
        this.list = data;

        let date = data.map(item => item.inspection_date).sort((a,b) => a > b ? 1 : -1);

        this.date.from = date[0];
        this.date.to = date[date.length - 1];
      });
  },
};
</script>

<style></style>
