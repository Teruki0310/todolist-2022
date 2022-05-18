<script setup>
import { ref } from "vue";

const todo = ref([
  { name: "やること1", price: "今日" },
  { name: "やること2", price: "明日" },
]);
const yatta = ref([]);
const newItemName = ref("寝る");
const newItemPrice = ref("今日");

const addItem = () => {
  if (newItemName.value != "") {
    todo.value.push({ name: newItemName.value, price: newItemPrice.value });
    newItemName.value = "寝る";
    newItemPrice.value = "今日";
  }
};
const addYatta = (index, name, price) => {
  yatta.value.push({ name: name, price: price });
  todo.value.pop(index);
};
const addTodo = (index, name, price) => {
  todo.value.push({ name: name, price: price });
  yatta.value.pop(index);
};
</script>

<template>
  <div>
    <div>やることリスト</div>
    <div v-for="(item, index) in todo" :key="item.name">
      <div class="item" :class="{ kyou: item.price == '今日' }">
        <div class="name">
          {{ index }} 　 {{ item.name }} 　 {{ item.price }}まで　　<button
            @click="addYatta(index, item.name, item.price)"
          >
            やった！
          </button>
        </div>
        <div v-if="item.name == 'ケモノ'">エッチだ...</div>
        <div v-if="item.name == 'ピカチュウ'">かわいい！！！！！</div>
        <div v-if="item.name == 500000000000">いつまでだよｗ5000兆</div>
        <div v-if="item.price == 500000000000">PIKACTF{NAZEBARETASI_PRO}</div>
        <div v-if="item.price == '昨日'">
          うおお～昨日試す人いた～～～～～！！！感動
        </div>
      </div>
    </div>
    <br />
    <br />
    <div>完了したタスク！</div>
    <div v-for="(item, index) in yatta" :key="item.name">
      <div class="item" :class="{ kyoudatta: item.price == '今日' }">
        <div class="name">
          {{ item.name }} 　 {{ item.price }}までだった　　<button
            @click="addTodo(index, item.name, item.price)"
          >
            †蘇生†
          </button>
        </div>
      </div>
    </div>
  </div>
  <div>
    <label>
      <br />
      <br />
      名前
      <input v-model="newItemName" type="text" />
    </label>
    <label>
      いつまで
      <input v-model="newItemPrice" type="text" />
    </label>
    <button @click="addItem">add</button>
  </div>
</template>

<style>
.kyou {
  color: red;
}
.kyoudatta {
  color: rgb(62, 136, 170);
}
</style>
