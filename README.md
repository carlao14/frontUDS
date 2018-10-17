# FRONT UDS - Avaliação

# Introducão

> Desenvolvido utilizando VUEJS, o projeto realiza um gerenciamento básico de cadastro, inserindo, alterando e excluindo os dados.  Foi utilizado axios para requisições HTTP e vue-notification para notificações . 

## Code Samples

<code>
    getCliente: function(){ <br />
           axios.get('http://127.0.0.1:8000/api/clientes')<br/>
                .then(response => (this.clientes = response.data));<br>}
</code>
<hr>
<code>
       addCliente: function(){<br/>
          let componente = this;<br/>
          axios.post('http://127.0.0.1:8000/api/clientes', {<br/>
                nome: componente.cliente.nome,<br/>
                email: componente.cliente.email<br/>
            })<br/>
            .then(function (response) {<br/>
                if(response.data.status == "OK"){<br/>
                    componente.notify("Dados salvos","Dados salvos com sucesso !");<br/>
                    componente.getCliente();<br/>
                    componente.cliente = {id:'',nome:'',email:''};<br/>
                }<br/>
            })<br/>
            .catch(function (error) {<br/>
                console.log(error);<br/>
            });<br/>}
</code>

# Instalação
<code> npm run serve </code>

O projeto precisa ser executado junto com a api disponivel nesse <a href ="https://github.com/carlao14/apiUDS"> <b>  link <b> </a>

* As URL's do projeto estão assumindo por padrão que o projeto Laravel sera executa em local host, para testes em produção altere as mesmas no arquivo Cliente.vue
<code> url:'http://127.0.0.1:8000/api/clientes' </code>
