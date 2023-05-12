<script setup>
import { ref } from 'vue';

const produtos = ref([
  {
    id: 1,
    nome: 'Camiseta',
    preco: 49.90,
    quantidade: 1
  },
  {
    id: 2,
    nome: 'Calça',
    preco: 99.90,
    quantidade: 1
  },
  {
    id: 3,
    nome: 'Meia',
    preco: 9.90,
    quantidade: 1
  },
  {
    id: 4,
    nome: 'Sapato',
    preco: 199.90,
    quantidade: 1
  }
])



let valortotal = ref(0)
let carrinho = ref([])


function addcarrinho(item) {
  carrinho.value.push({
    id: item.id,
    nome: item.nome,
    preco: item.preco,
    quantidade: item.quantidade,
    totalitem: item.preco * item.quantidade
  })
  totalvalor()
  item.quantidade = 1
}


function totalvalor() {
  valortotal.value = 0
  for (const item of carrinho.value) {
    valortotal.value = valortotal.value + item.totalitem
  }
}


function limpacarrinho() {
  carrinho.value = []
  valortotal.value = 0
}


function remover(index) {
  carrinho.value.splice(index, 1)
}

const pv = (value) => "R$ " + value.toFixed(2).replace('.', ',')
</script>

<template>
  <ul>
    <li class="produto" v-for="(item, index) in produtos" :key="index">
     <p>Item: {{ item.nome }}</p> 
     <p> Valor: {{ pv(item.preco) }}</p>
     <p> Quantidade: {{ item.quantidade }}</p>

      <button @click="addcarrinho(item)">adicionar ao carrinho</button>
      <button class="mais" @click="item.quantidade++">+</button>
      <button  class="menos" @click="item.quantidade--" v-if="item.quantidade > 0">-</button>
    </li>
  </ul>

  <div class="carrinho">
    <p class="car">carrinho: {{ pv(valortotal) }}</p>
    {{ carrinho.splice() }}
    <ul>

      <li v-for="(item, index) in carrinho" :key="index">
        <p>{{ item.nome }}</p>
        <p>{{ pv(item.preco) }}</p>
        <p>{{ item.quantidade }}</p> 
        <p>{{ pv(item.totalitem) }}</p>
        <button @click="remover(index)">remover</button>
      </li>
      <li v-for="(item, index) in carrinho" :key="index"> </li>
    </ul>

    <button @click="limpacarrinho()">limpa carrinho</button>
  </div>
</template>

<style scoped>
li {
  list-style: none;
}
.produto{
  width: 150px;
  border: 10px solid rgb(0, 0, 0);
  padding: 20px;
  margin: 5px;
}
.mais{
width: 30px;
align-items: center;
padding: 5px;
}
.menos{
width: 30px;
padding: 5px;
align-items: center;
}

</style>
