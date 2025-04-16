<script setup>
import { ref } from 'vue'

const userItems = ref([
  {
    "id": 1,
    "name": "Shoes 1"
  },
  {
    "id": 2,
    "name": "Shoes 2"
  },
  {
    "id": 3,
    "name": "Shoes 3"
  },
  {
    "id": 4,
    "name": "Shoes 4"
  },
  {
    "id": 5,
    "name": "T-shirt 1"
  },
  {
    "id": 6,
    "name": "T-shirt 2"
  },
  {
    "id": 7,
    "name": "T-shirt 3"
  },
  {
    "id": 8,
    "name": "T-shirt 4"
  }
])

const availableItems = ref([
  {
    "id": 11,
    "name": "Jacket 1"
  },
  {
    "id": 12,
    "name": "Jacket 2"
  },
  {
    "id": 13,
    "name": "Jacket 3"
  },
  {
    "id": 14,
    "name": "Jacket 4"
  },
  {
    "id": 15,
    "name": "Hoodie 1"
  },
  {
    "id": 16,
    "name": "Hoodie 2"
  },
  {
    "id": 17,
    "name": "Hoodie 3"
  },
  {
    "id": 18,
    "name": "Hoodie 4"
  }
])

const selectedUserItems = ref([])
const selectedAvailableItem = ref(null)

function toggleUserItem(item) {
  const index = selectedUserItems.value.findIndex((i) => i.id === item.id)
  if (index !== -1) {
    selectedUserItems.value.splice(index, 1)
  } else if (selectedUserItems.value.length < 6) {
    selectedUserItems.value.push(item)
  }
}

function selectAvailableItem(item) {
  selectedAvailableItem.value = item
}
</script>

<template>
  <div class="wrapper">
    <div>
      <h2>Выбранные вещи пользователя</h2>
      <p v-if="selectedUserItems.length === 0">Ничего не выбрано</p>
      <ul>
        <li class="event-none" v-for="item in selectedUserItems" :key="item.id">
          {{ item.name }}
        </li>
      </ul>
      <span>selected: {{selectedUserItems.length}} / 6</span>
    </div>


    <div>
      <h2>Выбранная вещь на выбор</h2>
      <p>{{ selectedAvailableItem?.name || 'Ничего не выбрано' }}</p>
    </div>

    <div>
      <h2>Вещи пользователя</h2>
      <ul>
        <li
            v-for="item in userItems"
            :key="item.id"
            @click="toggleUserItem(item)"
            :class="{ 'active': selectedUserItems.includes(item) }"
        >
          {{ item.name }}
        </li>
      </ul>
    </div>

    <div>
      <h2>Вещи на выбор</h2>
      <ul>
        <li
            v-for="item in availableItems"
            :key="item.id"
            @click="selectAvailableItem(item)"
        >
          {{ item.name }}
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 40px;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  border: 1px solid gray;
  padding: 10px;
  margin: 10px 0;
  cursor: pointer;
}
li.active {
  background: #535bf2;
}
.event-none {
  pointer-events: none;
}
</style>
