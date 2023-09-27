<template>

  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark border-bottom border-body">
            <div class="container-fluid">
                <router-link class="navbar-brand" to="/">Rick And Morty API Personagens</router-link>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
                    <div class="navbar-nav">
                      <li class="nav-item">
                        <router-link class="nav-link" aria-current="page" to="/">Home</router-link>                        
                      </li>
                    </div>
                </div>
            </div>
    </nav>
  </div>

  
  <div class="container texte-center">
    <div class="row">
        <div class="row col-12">
            <div v-for="c in personagem" style="margin-top: 5%;" class="col-6 mt-4 d-flex justify-content-center">
                <div class="col-sm-12 col-md-6">
                    <div id="card" style="background-color: #d7f7f4;" class="card">
                        <div  class="card-body row">
                            <div style="font-weight: bold; text-decoration: underline;" class=""><strong>{{ c.id }}</strong></div>
                            <div>
                                <p class="mt-4"> <strong>Nome do Personagem:</strong> {{ c.name }}</p>
                                <p class="mt-4"> <strong>Espécie:</strong> {{ c.species }}</p>
                                <p class="mt-4"> <strong>Origem:</strong> {{ c.origin.name }}</p>
                                <img :src = c.image width = "200" style = "margin-bottom: 20px;">                                
                                <button @click="infos(c)" type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">Outras Informações</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
  </div>

  <div v-if = 'lugar != null' class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog modal-xl">
      <div class="modal-content" style = "width : 650px;">
        <div style="background-color:rgb(0, 0, 0);" class="modal-header">
          <h1 class="modal-title fs-5" id="exampleModalLabel">Informações Adicionais</h1>
        </div>
        <div style="background-color: rgb(246, 250, 250);" class="modal-body">
            <div class="row">
              <div class="col-md-5"></div>
              <div>
                <h1 style="margin-left: 500px; font-weight: bold; text-decoration: underline;">{{this.name}}</h1>
            </div>
            <div style="margin-top: 5%;" class="col-12 mt-">
              <div class="col-sm-12 col-md-12 ">
                    <div id="card" class="card">
                        <div style="background-color: #ffffff;" class="card-body row">
                            <div  class=""><strong>Habitação : </strong>{{ lugar.name }}</div>
                            <div  class=""><strong>Estado : </strong>{{ estado }}</div>
                            <div  class=""><strong>Genero : </strong>{{ genero }}</div>
                            <div  class="" v-if ="tipo " ><strong>Tipo : </strong>{{ tipo }}</div>
                            <div v-else><strong>Tipo : </strong>Humano</div>
                        </div>
                    </div>
                </div>
            </div>
            </div>
        </div>
        <div style="background-color:rgb(255, 255, 255);" class="modal-footer">
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
      </div>
    </div>
  </div>



</template>

<script>
export default{
    data: function () {
        return {
            personagem: null,
            lugar: null,
            estado: null,
            tipo: null
        }
    },
    computed: {
    },
    methods: {
        getDados(){
            fetch("https://rickandmortyapi.com/api/character").then(res => { res.json().then((x) =>{ this.personagem = x.results })})
        },
        infos(c){
            this.name = c.displayName
            this.lugar = c.location
            this.estado = c.status
            this.genero = c.gender
            this.tipo = c.type
            console.log(c)
        },
        abreModal(){
            
        }
    },
    mounted: function () {
        this.getDados();
        
    }
}
</script>