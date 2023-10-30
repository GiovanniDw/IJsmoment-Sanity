<script setup>
const props = defineProps({
  data: Array,
  columns: Array,
  columnName: Array
})
</script>

<template>
  <div>
    <table v-show="data.length">
      <tbody>
        <tr v-for="(item, index) in columns" :key="index" :class="item">
          <th :class="item">
            {{ columnName[index] }}
          </th>
          <td v-for="entry in data" :key="entry.id" :class="entry.content.compare[0][item]">
            <span
              v-if="entry.content.compare[0][item] === true"
              class="icon material-symbols-rounded"
            >
              done
            </span>
            <span v-else> {{ entry.content.compare[0][item] }} </span>
          </td>
        </tr>
      </tbody>
    </table>
    <!-- <table class="table">
      <thead>
        <tr>
          <th v-for="(key, index) in columnName" :key="index">
            {{ key }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="entry in data">
          <td v-for="(key, index) in columns">
            <span
              v-if="entry.content.compare[0][key] === true"
              class="icon material-symbols-rounded"
            >
              done
            </span>
            <span v-else> {{ entry.content.compare[0][key] }} </span>
          </td>
        </tr>
      </tbody>
    </table> -->
  </div>
</template>

<style scoped lang="scss">
.icon {
  color: var(--color-primary);
}
table {
  width: 100%;
  // font-size: 14px;
  font-size: var(--step-0);
  tr {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    gap: 1em;
    margin-top: 1em;
    margin-bottom: 1em;
    // border-bottom: 0.0625em solid var(--color-gray);
  }

  th {
    text-align: right;
    // justify-self: center;
    font-size: 0.75em;
    line-height: 1;
  }
  td {
    font-size: 0.75em;
    text-align: center;
    justify-self: center;
  }
}

.title {
  th {
    opacity: 0;
  }
  td {
    font-size: 0.75em;
    padding: 0.25em 1em;
    background-color: var(--color-primary);
    border-radius: 25em;
    color: var(--color-text-inverse);
  }
  td:nth-child(4) {
    background-color: var(--color-primary);
  }
  td:nth-child(2) {
    background-color: var(--color-gray);
  }
  td:nth-child(3) {
    background-color: var(--color-accent);
  }
}

.table {
  display: flex;
  flex-direction: row;
  font-size: 1em;
  width: 100%;
  justify-content: space-between;

  thead tr {
    display: flex;
    flex-direction: column;
    justify-content: space-around;

    th {
      font-size: 1em;
    }
  }

  tbody {
    display: grid;
    flex-direction: row;
    grid-template-columns: 1fr 1fr 1fr;
    width: 100%;
  }

  tbody {
    overflow-x: scroll;
  }

  tbody tr {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
}
</style>
