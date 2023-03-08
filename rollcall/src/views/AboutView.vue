<template>
  <div class="wrapper">
    <div class="left">
      <ul>
        <li v-for="student in filteredItems" :key="student.id" @click="stu_id = student.name">{{ student.name }}</li>
      </ul>
    </div>
    <div class="right">
      <label for="stu_id">學生ID:</label>
      <input type="text" id="stu_id" v-model="stu_id" placeholder="學號" @keydown.enter="handleEnter"><br>
      <label for="card_id">卡片ID:</label>
      <input ref="cardInput" v-model="card_id" type="text" placeholder="Scan card here"
      @keydown.enter.prevent="submitInput" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      stu_id: '',
      card_id: '',
      students: [
        { id: 1, name: 'Apple' },
        { id: 2, name: 'Banana' },
        { id: 3, name: 'Orange' },
        { id: 4, name: 'Mango' }
      ],
      selectedStudent: ''
    }
  },
  methods: {
    
    submitInput() {
      // Do something with the input value
      console.log(this.inputValue);
    },
    handleEnter() {
      this.$refs.cardInput.focus()
    }
  },
  mounted() {
    this.$refs.cardInput.focus();
    this.$refs.cardInput.addEventListener('input', () => {
      if (this.inputValue.length === 10) {
        this.submitInput();
      }
    });
  },
  computed: {
    filteredItems() {
      return this.students.filter(students => students.name.toLowerCase().includes(this.stu_id.toLowerCase()));
    }
  }
}
</script>

<style scoped>
.wrapper {
  display: flex;
}

.left, .right {
  flex: 1;
  padding: 20px;
}


li {
  cursor: pointer;
  margin-bottom: 10px;
  padding: 10px;
  background-color: #f2f2f2;
  border-radius: 5px;
}

li:hover {
  background-color: #e6e6e6;
}

label {
  display: block;
  margin-bottom: 10px;
  font-weight: bold;
}

input[type="text"], select {
  padding: 5px;
  font-size: 16px;
  border-radius: 5px;
  border: 1px solid #ccc;
  margin-bottom: 10px;
  width: 100%;
}


</style>
