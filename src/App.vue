<template>
  <table>
    <tbody>
      <tr>
        <th>Date</th>
        <th>WeekDay</th>
        <th>In</th>
        <th>Out</th>
        <th>Lunch</th>
        <th>status</th>
        <th>+/-</th>
        <th>plan</th>
      </tr>
    </tbody>

    <Row
      @changed="updated"
      v-for="item in data"
      :dataSelect="item"
      :key="item"
    />
  </table>
  {{ sun }}
</template>

<script>
import Row from "@/components/Row.vue";
export default {
  data() {
    return {
      footer: 0,
      ArrayUpdated: [],
      sun: 0,
      data: [
        {
          selectedStatus: "",
          selectedIn: "",
          selectedLunch: "",
          selectedOut: "",
          id: Math.random().toString(36).substring(7),
        },
        {
          selectedStatus: "",
          selectedIn: "",
          selectedLunch: "",
          selectedOut: "",
          id: Math.random().toString(36).substring(7),
        },
        {
          selectedStatus: "",
          selectedIn: "",
          selectedLunch: "",
          selectedOut: "",
          id: Math.random().toString(36).substring(7),
        },
      ],
    };
  },
  components: {
    Row,
  },
  methods: {
    updated(footer) {
      this.ArrayUpdated = [
        ...this.ArrayUpdated.filter((item) => item.id !== footer.id),
        footer,
      ];
      this.footer = this.ArrayUpdated;
      this.sun = this.ArrayUpdated.reduce((acc, item) => {
        if (
          item.selectedOut == 0 ||
          item.selectedIn == 0
        ) {
          return acc;
        } else {
          let x =
            item.selectedOut > item.selectedIn
              ? item.selectedOut - item.selectedIn 
              : (item.selectedIn % 12) - item.selectedOut + 12   

          console.log(x)
          return acc + x;
        }
      }, 0);
    },
  },
};
</script>


<style >
table,
td,
th {
  border: 1px solid #ddd;
  text-align: left;
}

table {
  border-collapse: collapse;
  width: 100%;
}

th,
td {
  padding: 15px;
}
</style>