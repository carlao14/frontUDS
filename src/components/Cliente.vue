<template>
  <div class="container-fluid">
      <div class="row">
          <div class="col-5">
              <Painel v-bind:titulo="acao" >
                  <form class="form">
                    <div class="form-group">
                        <label for="nome" class="float-left">Nome</label>
                        <input type="text" v-model="cliente.nome" class="form-control">
                    </div>
                    <div class="form-group">
                        <label for="email" class="float-left">E-mail</label>
                        <input type="email" v-model="cliente.email" class="form-control"  placeholder="nome@example.com">
                    </div>
                    
                    <div class="form-group">
                        <div class="row">
                            <div class="col-6">
                                <button v-if="editar == false" type="button" v-on:click="addCliente()" class="btn btn-primary btn-block"> Cadastrar </button>
                                <button v-else type="button" v-on:click="updateCliente()" class="btn btn-primary btn-block"> Salvar </button>
                            </div>
                            <div class="col-6">
                                <button type="reset" class="btn btn-danger btn-block"> Limpar </button>
                            </div>
                        </div>
                    </div>                    
                </form>
              </Painel>
          </div>
          <div class="col-7">
              <Painel titulo="Listar" >
                 <table class="table table-hover table-striped">
                     <thead>
                         <tr>
                             <th>#</th>
                             <th>Nome</th>
                             <th>Email</th>
                             <th>Ação</th>
                         </tr>
                     </thead>
                     <tbody>
                         <tr v-for="cliente in clientes" v-bind:key="cliente.id">
                             <td>{{cliente.id}}</td>
                             <td>{{cliente.nome}}</td>
                             <td>{{cliente.email}}</td>
                             <td> 
                                 <i class="btn btn-sm btn-warning" v-on:click="edit(cliente)"> E </i> 
                                 <i class="btn btn-sm btn-danger" v-on:click="delet(cliente.id)"> X </i>
                             </td>
                         </tr>
                     </tbody>
                 </table>
              </Painel>
          </div>
      </div>
  </div>
</template>

<script>
import Painel from './../components/Painel.vue'
const axios = require('axios'); 


export default {
  nome: 'Cliente',
  components: {
    Painel
  },
  props: {
    msg: String
  },
  data: function() {
      return {
          url:'http://127.0.0.1:8000/api/clientes',
          editar: false,
          acao:"Cadastrar",
          cliente: {
              id:'',
              nome:'',
              email:''
          },
          clientes:[]
      }
  },
  mounted(){
      this.getCliente();
  },
  computed: { 
      
  },
  methods: {
      getCliente: function(){
        let componente = this;
           axios.get(componente.url)
                .then(response => (this.clientes = response.data));
                
      },
      notify: function(titulo,msg){
          this.$notify({
            group: 'foo',
            title: titulo,
            text: msg
            });
      },
      addCliente: function(){
          let componente = this;
          axios.post(componente.url, {
                nome: componente.cliente.nome,
                email: componente.cliente.email
            })
            .then(function (response) {
                if(response.data.status == "OK"){
                    componente.notify("Dados salvos","Dados salvos com sucesso !");
                    componente.getCliente();
                    componente.cliente = {id:'',nome:'',email:''};
                } 
            })
            .catch(function (error) {
                //console.log(error);
            });

      },
      edit: function(cliente){
          this.cliente = cliente;
          this.acao = "Alterar";
          this.editar = true;
      },
      updateCliente: function(){
          let componente = this;
          axios.put(componente.url+'/'+componente.cliente.id, {
                nome: componente.cliente.nome,
                email: componente.cliente.email
            })
            .then(function (response) {
                console.log(response.data);
                componente.notify("Dados salvos","Dados salvos com sucesso !");
                componente.getCliente();
                componente.cliente = {id:'',nome:'',email:''};
            })
            .catch(function (error) {
                //console.log(error);
            });
          this.acao = "Cadastrar";
          this.editar = false;
      },
      delet: function(id){
          let componente = this;
          axios.delete(componente.url+'/'+id)
            .then(function (response) {
                console.log(response.data);
                componente.notify("Cliente excluido","Cliente removido com sucesso!");
                componente.getCliente();
            })
            .catch(function (error) {
               // console.log(error);
            });
      }
  }
}
</script>
