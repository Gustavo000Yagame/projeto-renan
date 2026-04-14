<script setup lang="ts">
import { ref } from 'vue';
import 'bootstrap/dist/css/bootstrap.min.css';
import 'bootstrap/dist/js/bootstrap.bundle.min.js';

import type Funcionario from './models/Funcionario';

const ordem = ref('')
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
  const item = lista.value.find(item => item.id === id)
  if (item) {
    funcionario.value = { ...item }
    excluirFuncionario(id)
  }

}
  function ordenarCom() {
    if (ordem.value === 'salario')
      lista.value.sort((a, b) => a.salario - b.salario)
    else if (ordem.value === 'nome')
    lista.value.sort((a, b) => a.nome.localeCompare(b.nome))
    else if (ordem.value === 'cargo')
    lista.value.sort((a, b) => a.cargo.localeCompare(b.cargo))
  }




</script>

<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">SENAI</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link active" aria-current="page" href="#">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Sobre</a>
        </li>
        </ul>
    </div>
  </div>
</nav>




  <div class="container">
    <div class="row">
      <div class="col">
        <form @submit.prevent="salvaFuncionario">
          <div class="mb-3">
            <label for="nome" class="form-label">Nome</label>
            <input v-model="funcionario.nome" type="text" class="form-control" id="nome" required>
          </div>
          <div class="mb-3">
            <label for="preco" class="form-label">Email</label>
            <input v-model="funcionario.email" type="email" class="form-control" id="preco" required>
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

        <h4>Ordenação</h4>
        <select v-model="ordem" class="form-select" @change="ordenarCom" >
          <option value="nome">Nome</option>
          <option value="cargo">Cargo</option>
          <option value="salario">Salário</option>
        </select>

        <table class="table mt-3">
          <thead>
            <tr>
              <th scope="col">Nome</th>   
              <th scope="col">Email</th>
              <th scope="col">Cargo</th>
              <th scope="col">Salário</th>
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
              <button type="button" class="btn btn-warning" @click="editarFuncionario(item.id)">📝</button>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style>


.navbar {
  margin-left: 137px;
  display: flex;
  background-color: rgb(167, 167, 167);

}

body{
  background-color: #f8f9fa;
}


.h2 {
  margin-top: 30px;
}



</style>