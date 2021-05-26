<template>
  <q-page>
    <!-- Componente de tabela do Quasar: -->
    <!-- Columns: é onde iremos configurar as colunas da tabela
    Data: é onde vem os dados para serem exibidos na tabela -->
    <div class="row">
    <q-table
      grid
      title="Treats"
      :data="posts"
      :columns="columns"
      row-key="id"
      class="col"
      separator="cell"
      selection="single"
      :selected.sync="selected"
    />
    </div>
    {{selected}}
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',

  data () {
    return {
      // Colunas
      columns: [
        // Coluna 1
        {
          // Nome
          name: 'id',
          label: 'Id Post',
          field: 'id',
          align: 'left',
          // Como ele vai achar, através de pesquisa.
          // field: row => row.name,
          // format: val => `${val}`,
          // Para pesquisar por ordem
          sortable: true
        },
        // Coluna 2
        {
          // Nome
          name: 'title',
          label: 'Title',
          field: 'title',
          align: 'left',
          // Para pesquisar por ordem
          sortable: true
        }
      ],
      posts: [],
      selected: []
    }
  },
  // Disparar a API ao entrar na paǵina com a função mounted (ao montar o comp)
  mounted () {
    // Disparando a API
    this.getPosts()
  },

  // Funções ou métodos
  methods: {
    // Função para pegar os posts
    getPosts () {
      // Acessando o axios dentro do componente view
      // $axios foi definido como prototype, então sempre será chamado dessa forma
      this.$axios.get('https://jsonplaceholder.typicode.com/posts')
        // resposta (then):
        .then((res) => {
          // Alimentando o array de posts:
          this.posts = res.data // da resposta eu quero o data (res.data)
        })
        // caso der erro:
        .catch((err) => {
          console.log(err)
        })
    }
  }
}
</script>
