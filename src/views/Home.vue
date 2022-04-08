<template>
  <div class="box">
    <div class="box2">
      <h2>Введите текст для проверки:</h2>
      <div v-if="result!=null">
        <div v-if="result === true" class="positive">Позитивный текст</div>
        <div v-else class="negative">Негативный текст</div>
      </div>      <input class="inputRow" type="text" v-model="text"/>
      <button @click="sendText">Проверить</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      text: "",
      result: null,
    };
  },
  methods: {
      sendText(){
          axios
            .post('http://localhost:8080/model', {"text": this.text})
            .then(response => {
                console.log(response.data)
                this.result = response.data.result
            }).catch(error => {
                alert("Слова из текста не были найдены в модели")
            })
      }
  }
};
</script>

<style>
.box {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 1000px;
  width: 100%;
}
.box2 {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  align-items: center;
  height: 15%;
  width: 500px;
}
.inputRow {
  width: 50%;
}
button {
  height: 30px;
  width: 150px;
}
.positive {
    background-color: rgb(180, 236, 95)
}
.negative {
    background-color: rgb(255, 73, 73)
}
</style>
