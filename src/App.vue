<template>
  <div id="app">
    <h2>Alugueis</h2>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>ID Livro</th>
          <th>ID Usuário</th>
          <th>Data Aluguel Fim</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in alugueis" :key="item.id">
          <td>{{ item.id }}</td>
          <td>{{ item.livro_id }}</td>
          <td>{{ item.usuario_id }}</td>
          <td>{{ item.dt_aluguel_fim }}</td>
          <td>
            <button @click="excluirAluguel(item.id)">Excluir</button>
          </td>
        </tr>
      </tbody>
    </table>

    <h2>Usuários</h2>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Nome Usuário</th>
          <th>CPF Usuário</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in usuarios" :key="item.id">
          <td>{{ item.id }}</td>
          <td>{{ item.nome_usuario }}</td>
          <td>{{ item.cpf }}</td>
          <td>
            <button @click="excluirUsuario(item.id)">Excluir</button>
          </td>
        </tr>
      </tbody>
    </table>

    <h2>Livros</h2>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Nome Livro</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in livros" :key="item.id">
          <td>{{ item.id }}</td>
          <td>{{ item.nome_livro }}</td>
          <td>
            <button @click="excluirLivro(item.id)">Excluir</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      alugueis: [],
      usuarios: [],
      livros: []
    }
  },

  mounted() {
    this.getAlugueis()
    this.getUsuarios()
    this.getLivros()
  },

  methods: {
    async getAlugueis() {
      try {
        const response = await axios.get('http://localhost:8000/api/alugueis')
        this.alugueis = response.data
      } catch (error) {
        console.error('Erro ao obter os dados:', error)
      }
    },

    async getUsuarios() {
      try {
        const response = await axios.get('http://localhost:8000/api/usuarios')
        this.usuarios = response.data
      } catch (error) {
        console.error('Erro ao obter os dados:', error)
      }
    },

    async getLivros() {
      try {
        const response = await axios.get('http://localhost:8000/api/livros')
        this.livros = response.data
      } catch (error) {
        console.error('Erro ao obter os dados:', error)
      }
    },

    async excluirAluguel(id) {
      try {
        await axios.delete(`http://localhost:8000/api/aluguel/${id}`)
        this.getAlugueis()
      } catch (error) {
        console.error('Erro ao excluir o aluguel:', error)
      }
    },

    async excluirUsuario(id) {
      try {
        await axios.delete(`http://localhost:8000/api/usuario/${id}`)
        this.getUsuarios()
      } catch (error) {
        console.error('Erro ao excluir o usuário:', error)
      }
    },

    async excluirLivro(id) {
      try {
        console.log('aquiii', id)
        await axios.delete(`http://localhost:8000/api/livro/${id}`)
        this.getLivros()
      } catch (error) {
        console.error('Erro ao excluir o livro:', error)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}
</style>
