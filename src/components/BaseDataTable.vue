<template>
  <v-card
    class="pa-6 mx-auto"
    elevation="4"
    rounded="xl"
    max-width="1400"
  >

    <v-card-title class="text-h4 font-weight-bold text-primary mb-6">
      {{ title }}
    </v-card-title>

    <v-text-field
  v-model="search"
  label="Search"
  density="compact"
  hide-details
  class="mb-4"
/>

<div
  class="d-flex flex-wrap mb-4"
  style="gap:10px"
>

      <v-text-field
        v-for="column in columns"
        :key="column.key"
        v-model="newRow[column.key]"
        :label="column.title"
        density="compact"
        hide-details
      />

      <v-btn
        color="primary"
        @click="addRow"
      >
        Add
      </v-btn>

    </div>

    <v-table
      hover
      density="comfortable"
      class="rounded-lg"
    >

      <thead>

        <tr>

          <th
            v-for="column in columns"
            :key="column.key"
            @click="sort(column.key)"
            class="table-header"
          >

            {{ column.title }}

            <span v-if="sortKey === column.key">
              {{ ascending ? "▲" : "▼" }}
            </span>

          </th>

          <th class="table-header">
            Actions
          </th>

        </tr>

      </thead>

      <tbody>

<tr v-if="paginatedItems.length === 0">
  <td :colspan="columns.length + 1" class="text-center">
    No data available
  </td>
</tr>

<tr
  v-for="item in paginatedItems"
  :key="item.id"
>

          <td
            v-for="column in columns"
            :key="column.key"
          >
            {{ item[column.key] }}
          </td>

          <td>

  <v-btn
    color="primary"
    size="small"
    class="mr-2"
    @click="openEdit(item)"
  >
    Edit
  </v-btn>

  <v-btn
    color="error"
    size="small"
    @click="deleteRow(item.id)"
  >
    Delete
  </v-btn>

</td>
        </tr>

      </tbody>

    </v-table>

    <div
      class="d-flex justify-center align-center mt-6"
      style="gap:20px"
    >

      <v-btn
        variant="outlined"
        @click="previousPage"
        :disabled="page===1"
      >
        Previous
      </v-btn>

      <span class="font-weight-medium">
        Page {{ page }} / {{ totalPages }}
      </span>

      <v-btn
        variant="outlined"
        @click="nextPage"
        :disabled="page===totalPages"
      >
        Next
      </v-btn>

    </div>
    <v-dialog
  v-model="editDialog"
  max-width="500"
>
  <v-card>

    <v-card-title>Edit Record</v-card-title>

    <v-card-text>

      <v-text-field
        v-for="column in columns"
        :key="column.key"
        v-model="editedRow[column.key]"
        :label="column.title"
        density="compact"
      />

    </v-card-text>

    <v-card-actions>

      <v-spacer />

      <v-btn
        text
        @click="editDialog = false"
      >
        Cancel
      </v-btn>

      <v-btn
        color="primary"
        @click="saveEdit"
      >
        Save
      </v-btn>

    </v-card-actions>

  </v-card>
</v-dialog>

<v-dialog
  v-model="deleteDialog"
  max-width="400"
>
  <v-card>

    <v-card-title>Delete Record</v-card-title>

    <v-card-text>
      Are you sure you want to delete this record?
    </v-card-text>

    <v-card-actions>

      <v-spacer />

      <v-btn
        text
        @click="deleteDialog = false"
      >
        Cancel
      </v-btn>

      <v-btn
        color="red"
        @click="confirmDelete"
      >
        Delete
      </v-btn>

    </v-card-actions>

  </v-card>
</v-dialog>

  </v-card>
</template>

<script setup>

import {
  ref,
  computed,
  watch
} from "vue"

const props = defineProps({
  title: String,
  columns: Array,
  items: Array
})

const tableItems = ref([])
const newRow = ref({})
const search = ref("")

const editDialog = ref(false)
const deleteDialog = ref(false)

const editedRow = ref({})
const selectedRow = ref(null)


watch(
  () => props.items,
  (value) => {

    const saved = localStorage.getItem(props.title)

    tableItems.value = saved
      ? JSON.parse(saved)
      : [...value]

  },
  {
    immediate: true
  }
)

const sortKey = ref("")
const ascending = ref(true)

function sort(key) {

  if (sortKey.value === key) {
    ascending.value = !ascending.value
  }

  else {

    sortKey.value = key
    ascending.value = true

  }

}

const sortedItems = computed(() => {

  if (!sortKey.value)
    return tableItems.value

  return [...tableItems.value].sort((a, b) => {

    if (a[sortKey.value] < b[sortKey.value])
      return ascending.value ? -1 : 1

    if (a[sortKey.value] > b[sortKey.value])
      return ascending.value ? 1 : -1

    return 0

  })
})

  const filteredItems = computed(() => {

  if (!search.value) {
    return sortedItems.value
  }

  return sortedItems.value.filter(item =>
    Object.values(item).some(value =>
      String(value)
        .toLowerCase()
        .includes(search.value.toLowerCase())
    )
  )

})


const page = ref(1)

const rowsPerPage = 10

const totalPages = computed(() =>
  Math.ceil(
    filteredItems.value.length / rowsPerPage
  )
)

const paginatedItems = computed(() => {

  const start =
    (page.value - 1) * rowsPerPage

  return filteredItems.value.slice(
    start,
    start + rowsPerPage
  )

})

function nextPage() {

  if (page.value < totalPages.value){
    page.value++
  }
}

function previousPage() {

  if (page.value > 1){
    page.value--
  }
}

function addRow() {
  if (Object.keys(newRow.value).length === 0) return
  const row = {
    id: Date.now()
  }

  props.columns.forEach(column => {
    row[column.key] = newRow.value[column.key] || ""
  })

  tableItems.value.push(row)
  page.value = 1
  newRow.value = {}

}

function openEdit(item) {

  if(!item) return

  editedRow.value = { ...item }
  selectedRow.value = item.id
  editDialog.value = true

}

function saveEdit() {

  const index = tableItems.value.findIndex(
    item => item.id === editedRow.value.id
  )

  if (index !== -1) {

    tableItems.value[index] = {
      ...editedRow.value
    }

  }

  editDialog.value = false
  editedRow.value = {}

}

function deleteRow(id) {

  selectedRow.value = id
  deleteDialog.value = true

}

function confirmDelete() {

  tableItems.value = tableItems.value.filter(
    item => item.id !== selectedRow.value
  )

  deleteDialog.value = false
  selectedRow.value = null

if (page.value > totalPages.value) {
  page.value = totalPages.value
}

}
watch(
  tableItems,
  (value) => {
    localStorage.setItem(
      props.title,
      JSON.stringify(value)
    )
  },
  {
    deep: true
  }
)

</script>

<style scoped>

.table-header {
  background-color: rgb(var(--v-theme-primary));
  color: white;
  font-weight: 700;
  letter-spacing: 0.5px;
  padding: 14px;
  cursor: pointer;
}

.table-header:hover {
  background-color: #eeeeee;
}
</style>