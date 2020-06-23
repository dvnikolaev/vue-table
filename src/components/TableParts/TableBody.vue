<template>
  <tbody>
    <tr
      v-for="(item, i) in list"
      :key="i"
      :class="colorRow(item.inspection_description)"
    >
    <td 
      v-for="col in columns"
      :key="col.value"
      v-show="col.visible">
      {{ item[col.value] }}
    </td>
    </tr>
  </tbody>
</template>

<script>
export default {
  props: {
    list: Array,
    columns: Array
  },
  methods: {
    colorRow(val) {
      const value = val.toLowerCase().trim();
      switch (value) {
        case "no action":
          return "bg--red";
        case "reinspection required":
          return 'bg--yellow'
        case 'shorter date advance':
          return 'bg--blue'
        case 'issued permit':
          return 'bg--green'
        default:
          return "";
      }
    },
  },
};
</script>

<style>
.bg--red {
  background-color: orangered;
}
.bg--yellow {
  background-color: khaki;
}
.bg--blue {
  background-color:dodgerblue;
}
.bg--green {
  background-color: springgreen;
}
</style>
