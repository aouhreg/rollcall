<template>
  <div class="hello">
    <h1>點名</h1>
    <p>現在時間是：<span id="time"></span></p>
    <p v-if="msg === ''">{{name}},點名成功</p>
    <p v-else-if="msg === 'bad'">{{ name }},你遲到了</p>
    <p v-else-if="msg === 'no'">{{ name }},下次請早</p>
    <div>
      <input v-model="inputValue" type="text" placeholder="讀取卡片或者輸入學號" @keydown.enter="submitInput" autofocus/>
      <button @click="submitInput">確認</button>
  </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
    name: String
  },
  data() {
    return {
      inputValue: ''
    }
  },
  methods: {
    submitInput() {
      // Do something with the input value
      console.log(this.inputValue);
      alert(this.inputValue);
      location.reload();
    }
  }
}

function updateTime() {
  var now = new Date();
  var hours = now.getHours();
  var minutes = now.getMinutes();
  var seconds = now.getSeconds();

  if (hours < 10) {
    hours = "0" + hours;
  }
  if (minutes < 10) {
    minutes = "0" + minutes;
  }
  if (seconds < 10) {
    seconds = "0" + seconds;
  }

  var timeString = hours + ":" + minutes + ":" + seconds;
  document.getElementById("time").innerHTML = timeString;
}

setInterval(updateTime, 1000);



</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
button {
  background-color: #000000; /* Green */
  border: none;
  color: white;
  padding: 11px 16px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 8px;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 10px;
}
input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
}

</style>
