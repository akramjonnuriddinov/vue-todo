<template>
  <div class="p-4 container max-w-[500px] w-full mx-auto shadow">
    <h1 class="text-center text-2xl text-bold mb-2">Todo</h1>
    <form class="flex gap-2 mb-2" @submit.prevent="addUsers">
      <input
        class="border w-full p-1 rounded focus:outline-blue-500"
        v-model="input_value"
        type="text"
      />
      <button
        type="button"
        @click="addUsers()"
        class="border px-4 py-1 bg-green-700 rounded text-white"
      >
        add
      </button>
    </form>

    <ul class="w-full">
      <li
        v-for="(user, index) in users"
        :key="index"
        class="mb-2 flex justify-between border-b items-center"
      >
        <p>{{ index }} {{ user.text }}</p>
        <button
          @click="deleteUser(index)"
          class="border bg-red-400 text-white px-2 py-1 rounded"
        >
          delete
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      users: [],
      input_value: ''
    }
  },
  mounted() {
    this.users = JSON.parse(localStorage.getItem('users'))
      ? JSON.parse(localStorage.getItem('users'))
      : []
  },
  methods: {
    setUsers() {
      localStorage.setItem('users', JSON.stringify(this.users))
    },
    addUsers() {
      this.users.push({ text: this.input_value, completed: false })
      this.setUsers()
      this.input_value = ''
    },
    deleteUser(index) {
      this.users.splice(index, 1)
      this.setUsers()
    }
  }
}
</script>
