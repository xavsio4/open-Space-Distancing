<template>
  <b-container>
    <b-row>
      <b-col>
        <table class="table table-bordered">
          <tbody>
            <tr v-for="(item, index) in rows" :key="index">
              <td
                v-for="(column, indexColumn) in item"
                :key="indexColumn"
                :data-column="indexColumn"
                :data-row="index"
                class="member"
                :id="(index + 1) * 10 + indexColumn"
              >
                <a v-if="column != ''" @click="selectMember">{{ column }}</a>
                <span v-else></span>
              </td>
            </tr>
          </tbody>
        </table>
      </b-col>
      <b-col>
        <v-card>
          <div>
            <label for="example-datepicker">Date de la liste</label>
            <b-form-datepicker
              id="example-datepicker"
              v-model="datePresent"
              class="mb-2"
            ></b-form-datepicker>
          </div>
          <h3>Seront présents en date du {{ datePresent }}</h3>

          <ul>
            <li v-for="item in selectedCell">
              {{ item }}
            </li>
          </ul>
        </v-card>
      </b-col>
    </b-row>
  </b-container>
</template>
<script>
//import MemberCompo from "./MemberCompo.vue";
//import print from "print-js";

export default {
  components: {
    // MemberCompo
  },
  data() {
    return {
      datePresent: null,
      output: "",
      members: [],
      grid: [9, 14], //col,rows
      rows: [
        ["PT", "DR", "", "", "AS", "", "", "BS", ""],
        ["", "", "", "", "", "", "", "", ""],
        ["", "", "", "", "", "", "", "LC", ""],
        ["", "", "", "", "", "", "", "", ""],
        ["", "", "", "", "", "", "", "", ""],
        ["", "", "", "", "", "", "GP", "", "RO"],
        ["", "", "", "", "", "", "", "", "PM"],
        ["", "", "", "", "", "", "", "", ""],
        ["", "", "", "", "", "", "RI", "", "DC"],
        ["", "", "", "", "", "", "XV", "", "JP"],
        ["", "", "", "", "", "", "", "", ""],
        ["", "", "", "", "", "", "NR", "", "GL"],
        ["", "", "", "", "", "", "JL", "", "IR"],
        ["", "", "", "", "", "", "", "", "LM"]
      ],
      selectedCell: [],
      incompatible: []
    };
  },
  methods: {
    tablefinder(pos, index) {
      if (index >= 0) {
        if (pos - 1 > this.grid[0])
          document.getElementById(pos - 1).classList.remove("forbidden");

        if ((pos % 10) + 1 != this.grid[0])
          document.getElementById(pos + 1).classList.remove("forbidden");

        if (pos - 10 > 10)
          document.getElementById(pos - 10).classList.remove("forbidden");

        if (pos + 10 < this.grid[1] * 10 + 9)
          document.getElementById(pos + 10).classList.remove("forbidden");
      } else {
        if (pos - 1 > 9)
          document.getElementById(pos - 1).classList.add("forbidden");

        if ((pos % 10) + 1 != 9)
          document.getElementById(pos + 1).classList.add("forbidden");

        if (pos - 10 > 10)
          document.getElementById(pos - 10).classList.add("forbidden");

        if (pos + 10 < this.grid[1] * 10 + 9)
          document.getElementById(pos + 10).classList.add("forbidden");
      }
    },
    selectMember(e) {
      const index = this.selectedCell.findIndex(t => t == e.target.text);

      if (index >= 0) {
        this.selectedCell.splice(index, 1);
        e.target.classList.remove("active");
      } else {
        this.selectedCell.push(e.target.text);
        e.target.classList.add("active");
      }

      this.tablefinder(e.target.parentNode.id * 1, index);
    }
  }
};
</script>
<style>
.member {
  cursor: pointer;
  font-weight: 900;
}

.active {
  background-color: lightgreen;
}

.forbidden {
  background-color: red;
  color: white;
}

.forbidden a {
  pointer-events: none;
  cursor: default;
  text-decoration: none;
  color: black;
}
</style>
