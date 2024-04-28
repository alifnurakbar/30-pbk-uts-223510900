<template>
  <div>
    <h1>Daftar Bacaan Komik</h1>
    <button @click="showAll = !showAll">
      {{ showAll ? 'Tampilkan yang belum Dibaca' : 'Tampilkan Semua' }}
    </button>
    <ul>
      <li v-for="(activity, index) in filteredActivities" :key="index">
        <div class="activity-item">
          <input type="checkbox" v-model="activity.completed" />
          <span :class="{ completed: activity.completed }">{{ activity.text }}</span>
          <button @click="cancelActivity(index)">Hapus</button>
        </div>
      </li>
    </ul>
    <input v-model="newActivity" @keyup.enter="addActivity" placeholder="Tambahkan buku komik" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      activities: [],
      newActivity: '',
      showAll: true, 
    };
  },
  computed: {
    filteredActivities() {
      if (this.showAll) {
        return this.activities;
      } else {
        return this.activities.filter(activity => !activity.completed);
      }
    },
  },
  methods: {
    addActivity() {
      if (this.newActivity.trim() !== '') {
        this.activities.push({ text: this.newActivity, completed: false });
        this.newActivity = '';
      }
    },
    cancelActivity(index) {
      this.activities.splice(index, 1);
    },
  },
};
</script>

<style scoped>
h1 {
  font-size: 24px;
  color: white;
  margin-bottom: 20px;
}


button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 8px 16px;
  cursor: pointer;
  font-size: 14px;
  margin-right: 10px;
}

li {
  list-style: none;
  margin-bottom: 10px;
}

.activity-item {
  display: flex;
  align-items: center;
  margin-left: 10px;
}

li.completed span {
  text-decoration: line-through;
  color: #888;
}

input[type="checkbox"] {
  margin-right: 10px;
}
</style>
