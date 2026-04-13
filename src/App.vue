<script setup lang="ts">
import { ref } from 'vue';
import 'bootstrap/dist/css/bootstrap.min.css';
import 'bootstrap/dist/js/bootstrap.bundle.min.js';

import type Funcionario from './models/Funcionario';

const funcionario = ref({} as Funcionario)
const lista = ref([] as Funcionario[])

function salvaFuncionario() {
  lista.value.push(funcionario.value)
  funcionario.value = {} as Funcionario
}

function excluirFuncionario(id: number) {
  lista.value = lista.value.filter(item => item.id !== id)
}

function editarFuncionario(id: number) {

}


</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <form @submit.prevent="salvaFuncionario">
          <div class="mb-3">
            <label for="nome" class="form-label">Nome</label>
            <input v-model="funcionario.nome" type="text" class="form-control" id="nome">
          </div>
          <div class="mb-3">
            <label for="preco" class="form-label">Email</label>
            <input v-model="funcionario.email" type="email" class="form-control" id="preco">
          </div>
          <div class="mb-3">
            <label for="desc" class="form-label">Cargo</label>
            <input v-model="funcionario.cargo" type="text" class="form-control" id="desc">
          </div>
          <div class="mb-3">
            <label for="desc" class="form-label">Salario</label>
            <input v-model="funcionario.salario" type="number" class="form-control" id="desc">
          </div>
          <button type="submit" class="btn btn-primary">Salvar</button>
        </form>
        <table class="table mt-3">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Nome</th>   
              <th scope="col">Email</th>
              <th scope="col">Cargo</th>
              <th scope="col">Salario</th>
              <th scope="col">Ações</th>

            </tr>
          </thead>
          <tbody>
            <tr v-for="item in lista" :key="item.nome">
              <th scope="row">{{ item.id }}</th>
              <td>{{ item.nome }}</td>
              <td>{{ item.email }}</td>
              <td>{{ item.cargo }}</td>
              <td>{{ item.salario }}</td>


              <button type="button" class="btn btn-danger" @click="excluirFuncionario(item.id)">🗑️</button>
              <button type="button" class="btn btn-warning">📝</button>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style>

body{
  background-color: #f8f9fa;
  margin-top: 50px;
}

</style>