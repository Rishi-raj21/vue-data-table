<template>
  <v-card
    class="pa-4"
    elevation="0"
  >

    <v-card-title class="text-h5 font-weight-bold mb-4">
      {{ title }}
    </v-card-title>


    <v-table hover>

      <thead>
        <tr>

          <th
            v-for="column in columns"
            :key="column.key"
            @click="sort(column.key)"
            class="text-left cursor-pointer"
          >

            {{ column.title }}

            <span v-if="sortKey === column.key">
              {{ ascending ? "▲" : "▼" }}
            </span>

          </th>

        </tr>
      </thead>


      <tbody>

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


  </v-card>
</template>

<script setup>
import { ref, computed } from "vue"

const props = defineProps({
  title: String,
  columns: Array,
  items: Array
})

const sortKey = ref("")
const ascending = ref(true)

function sort(key) {
  if (sortKey.value === key) {
    ascending.value = !ascending.value
  } else {
    sortKey.value = key
    ascending.value = true
  }
}

const sortedItems = computed(() => {
  if (!sortKey.value) return props.items

  return [...props.items].sort((a, b) => {
    if (a[sortKey.value] < b[sortKey.value])
      return ascending.value ? -1 : 1

    if (a[sortKey.value] > b[sortKey.value])
      return ascending.value ? 1 : -1

    return 0
  })
})

const page = ref(1)

const rowsPerPage = 10

const totalPages = computed(() =>
  Math.ceil(sortedItems.value.length / rowsPerPage)
)

const paginatedItems = computed(() => {
  const start = (page.value - 1) * rowsPerPage

  return sortedItems.value.slice(
    start,
    start + rowsPerPage
  )
})

function nextPage() {
  if (page.value < totalPages.value)
    page.value++
}

function previousPage() {
  if (page.value > 1)
    page.value--
}
</script>