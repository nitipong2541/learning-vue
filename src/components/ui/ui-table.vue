<template>
  <table>
    <thead>
      <tr>
        <td
          v-for="col in cols"
          :key="col.id"
          class="border-2 border-indigo-800"
          :class="[col.text == '' ? null : 'w-30']"
        >
          {{ col.text }}
        </td>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(row, idx) in rows" :key="idx">
        <td
          v-for="col in cols"
          :key="col.id"
          class="border-2 border-l-gray-600 border-r-gray-600"
        >
          <slot v-if="row.editmode" :name="col.id" :row="row" :col="col" :idx="idx">
            <input
              v-if="col.id == 'date'"
              type="date"
              class="w-30"
              v-model="row[col.id]"
            />
            <input
              v-else-if="col.id == 'age'"
              type="number"
              class="w-30"
              v-model="row[col.id]"
            />
            <input v-else v-model="row[col.id]" />
          </slot>
          <slot v-else :name="col.id" :row="row" :col="col" :idx="idx">{{
            row[col.id]
          }}</slot>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    rows: {
      type: Array,
      default() {
        return [];
      },
    },
    cols: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  computed: {
    chackLog() {
      console.log(rows);
      return;
    },
  },
};
</script>
