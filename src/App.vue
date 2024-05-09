<template>
  <div>
    <h1>Catatan Tugas</h1>
    <form>
      <label for="activity">Tugas:</label>
      <input type="text" id="activity" v-model="newActivity"><br><br>
      <button type="button" @click="addActivity">Tambah</button>
      <button type="button" @click="filterUnfinished">Filter Halaman</button>
    </form>
    <ul>
      <li v-for="(activity, index) in activities" :key="index" :style="{textDecoration: activity.completed ? 'line-through' : 'none'}">
        {{ activity.name }}
        <button @click="removeActivity(index)">Hapus</button>
        <button @click="completeActivity(index)" v-if="!activity.completed">Selesai</button>
        <button @click="editActivity(index)">Edit</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activities: [],
      newActivity: "",
    };
  },
  methods: {
    addActivity() {
      if (this.newActivity !== "") {
        this.activities.push({ name: this.newActivity, completed: false });
        this.newActivity = "";
      }
    },
    removeActivity(index) {
      this.activities.splice(index, 1);
    },
    completeActivity(index) {
      this.activities[index].completed = true;
    },
    filterUnfinished() {
      this.activities = this.activities.filter(function (activity) {
        return !activity.completed;
      });
    },
    editActivity(index) {
      const newName = prompt("Masukkan nama baru untuk tugas:");
      if (newName !== null && newName.trim() !== "") {
        this.activities[index].name = newName;
      }
    },
  },
};
</script>


<style>
body {
  background: url('/src/bground.jpeg') no-repeat center center fixed;
  background-size: cover;
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
}

h1 {
  color: #333;
  margin-top: 50px;
  text-align: center;
}

form {
  margin: 20px auto;
  text-align: center;
}

label {
  display: inline-block;
  margin-right: 10px;
  text-align: right;
  width: 80px;
}

input[type="text"] {
  border: 2px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  font-size: 16px;
  margin: 5px 0;
  padding: 10px;
  width: 200px;
}

button {
  background-color: #007bff;
  border: none;
  border-radius: 4px;
  color: white;
  cursor: pointer;
  font-size: 16px;
  margin: 5px;
  padding: 10px 20px;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #0056b3;
}

ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

li {
  background-color: #8b4513;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-bottom: 10px;
  padding: 10px;
  position: relative;
}

li button {
  background-color: #dc3545;
  border: none;
  border-radius: 4px;
  color: white;
  cursor: pointer;
  font-size: 14px;
  padding: 5px 10px;
  position: absolute;
  right: 5px;
  top: 50%;
  transform: translateY(-50%);
}

li button:last-child {
  background-color: #28a745;
  right: 65px;
}

li button:hover {
  background-color: #c82333;
}

li button:last-child:hover {
  background-color: #218838;
}

li.completed {
  text-decoration: line-through;
  background-color: #6c757d;
  color: #fff;
}
</style>