<script setup>
import { onMounted, ref } from 'vue';
const title = ref("Vue Project");
const status = ref("pending");
const list = ref(["one", "two", "three"]);
const newTask = ref("");


const toggleStatus = () => {
  if (status.value === "active")
    status.value = "pending"
  else if (status.value === "pending")
    status.value = "inactive"
  else status.value = "active";
}

const addTask = () => {
  if (newTask.value.trim() !== '') {
    console.log(newTask.value);
    list.value.push(newTask.value)
    console.log(list.value)
    newTask.value = "";
  }
}

const deleteTask = (index) => {
  list.value.splice(index, 1);
}

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos")
    const data = await response.json();
    list.value = data.map((task) => task.title)
  } catch (error) {
    console.log(error)
  }
})
</script>

<template>
  <h1>{{ title }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>user is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">New Task</label>
    <br>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <p>List</p>
  <ul>
    <li v-for="(data, index) in list" :key="data">
      <span>
        {{ data }}
      </span>
      <button @click="deleteTask(index)">X</button>
    </li>
  </ul>
  <a :href="link" :target="_blank">Click here</a>
  <br />
  <button v-on:click="toggleStatus">Toggle Status</button>
</template>


<!-- <script>
export default {
  data: () => {
    return {
      title: "Vue Project",
      status: "pending",
      list: ["one", "two", "three"],
      link: "https://google.com",
    };
  },
  methods: {
    toggleStatus() {
      if (this.status === "active")
        this.status = "pending"
      else if (this.status === "pending")
        this.status = "inactive"
      else this.status = "active";

    }

    ,
  },
};
</script>

<template>
  <h1>{{ title }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>user is inactive</p>

  <p>List</p>
  <ul>
    <li v-for="data in list" :key="data">{{ data }}</li>
  </ul>
  <a :href="link" :target="_blank">Click here</a>
  <br />
  <button v-on:click="toggleStatus">Toggle Status</button>
</template> -->
