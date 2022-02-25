<template>
  <nav class="navbar" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <a class="navbar-item" href="/">
        <span class="is-hidden">Vuedex</span>
        <figure>
          <img src="../assets/logo.png" alt="Vuedex Logotipo" title="Vuedex"> 
        </figure>
      </a>

      <a role="button" :class="{'navbar-burger': true, 'is-active' : showNav }" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample" v-on:click="showNav = !showNav">
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        <span class="is-hidden">Vuedex</span>
      </a>
    </div>

    <div id="navbarBasicExample" :class="{'navbar-menu': true, 'is-active': showNav}">
      <div class="navbar-start">
        <a class="navbar-item has-text-primary has-text-weight-bold" href="/">
          Vuedéx
        </a>
        <div class="navbar-item has-dropdown is-hoverable">
          <a class="navbar-link">
            Acerca do projeto
          </a>

          <div class="navbar-dropdown">
            <a class="navbar-item" href="https://github.com/eng-gabrielscardoso/vuedex" target="_blank">
              <i class="fa fa-github mr-1" aria-hidden="true"></i>
              Documentação
            </a>
            <a class="navbar-item" href="https://linkedin.com/in/eng-gabrielscardoso" target="_blank">
              <i class="fa fa-linkedin mr-1" aria-hidden="true"></i>
              Portfólio pessoal
            </a>
            <hr class="navbar-divider">
            <a class="navbar-item" href="https://github.com/eng-gabrielscardoso/vuedex/issues/new" target="_blank">
              <i class="fa fa-exclamation-triangle mr-1" aria-hidden="true"></i>
              Reportar erro
            </a>
          </div>
        </div>
      </div>

      <div class="navbar-end">
        <div class="navbar-item">
          <input class="input is-primary mr-1" type="text" name="searchInput" id="searchInput" placeholder="Buscar Pokemon" aria-label="Buscar Pokemon" v-model="query">
          <div class="buttons">
            <button class="button is-primary is-fullwidth" @click="getQuery()">Pesquisar</button>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
  props: {
    title: String,
  },
  data() {
    return {
      query: '',
      showNav: false,
    }
  },
  methods: {
    getQuery() {
      console.log('Emitindo do filho: ' + this.query);
      let filteredQuery = this.query.toLowerCase();
      this.$emit('getQuery', filteredQuery );
    }
  },
}
</script>

<style>
  @media screen and (max-width: 1024px) {
    input[type=text] {
      margin-bottom: 6px !important;
    }
  }
</style>