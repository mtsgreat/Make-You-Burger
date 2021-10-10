<template>
    <Msg :exibirMsg="exibirMsg" v-show="exibirMsg"/>
    <div id="burger-table">
        <div>
            <div id="burger-table-heading">
                <div class="order-id">#:</div>
                <div>Cliente:</div>
                <div>Pão:</div>
                <div>Carne:</div>
                <div>Opcionais:</div>
                <div>Ações:</div>
            </div>
            <div class="burger-table-rows" v-for="burger in burgers" :key="burger.id">
                <div class="burger-table-row">
                    <div class="order-number">{{ burger.id }}</div>
                    <div>{{ burger.nome }}</div>
                    <div>{{ burger.pao }}</div>
                    <div>{{ burger.carne}}</div>
                    <div>
                        <ul>
                            <li v-for="(opcao,index) in burger.opacionais" :key="index" >{{opcao}}</li>
                           
                        </ul>
                    </div>
                    <div>
                        <select name="status" id="status" @change="updateBurger($event, burger.id)">
                            <option :value="status.tipo" v-for="status in dadosStatus" :key="status.id" :selected="burger.status == status.tipo ">{{status.tipo}}</option>
                            
                        </select>
                        <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
                    </div>
                </div>
            </div>  
        </div>
    </div>


 
</template>


<script>

import Msg from './Msg.vue'

export default {
   name: "Dashboard",
   components: {
       Msg
   },
   data(){
       return {
           dadosStatus: [],
           burgers: [],
           exibirMsg: null
        
       }
   },
   methods: {
       async getStatus(){
           const req = await fetch("http://localhost:3000/status");
           const data = await req.json();
           this.dadosStatus = data
       },

       async getBurgers(){
           const req = await fetch("http://localhost:3000/burgers");
           const data = await req.json();

          this.burgers = data;
         
       },

       async deleteBurger(id){
           const req = await fetch(`http://localhost:3000/burgers/${id}`, {
               method: "DELETE"
           });

           const res = await req.json();

           //msg de delete
           this.exibirMsg = `O pedido N°${id} foi exluido com sucesso!!`

           setTimeout(()=> {
               this.exibirMsg = false
           },3000)

           // ao chamar o this.getBurgers vai forcar uma atualização do Json, atualizando
           this.getBurgers();

       },
       async updateBurger(event, id){

           //pegando o valor q o usuario selecionou no select
           const option = event.target.value;

            //transformando o Json em String
           const dataJson = JSON.stringify({ status: option });

           //fazendo requisião de atualização
           const req = await fetch(`http://localhost:3000/burgers/${id}`, {
               method: "PATCH",
               headers: {"Content-Type": "application/json"},
               body: dataJson
           });

           const res = await req.json();

           console.log(res);

           //msg de atualização do status do pedido
           this.exibirMsg = `O pedido N°${id} foi atualizado para ${res.status}`;
           setTimeout(()=> {
               this.exibirMsg = false;
           },3000)
       }
   },
   mounted() {
       this.getStatus();
       this.getBurgers();

   }
}
</script>


<style scoped>

    #burger-table{
        max-width: 1200px;
        margin: 0 auto;
    }

    #burger-table-heading,
    .burger-table-rows,
    .burger-table-row{
        display: flex;
        /* flex-wrap: wrap; */
    }


    #burger-table-heading{
        font-weight: bold;
        padding: 12px;
        border-bottom: solid 3px #333;
    }

    #burger-table-heading div,
    .burger-table-row div {
        width: 20%;
    }

    .burger-table-row {
        width:  100%;
        padding: 12px;
        border-bottom: 1px solid #ccc;
    }


    #burger-table-heading .order-id,
    .burger-table-row .order-number{
        width: 5%;
    }

    select{
        padding: 12px 6px;
        margin-right: 12px;
    }


    .delete-btn{
         background-color: var(--primary-color);
            color: var(--secundary-color);
            font-weight: bold;
            border: 2px solid var(--primary-color);
            padding: 10px;
            font-size: 16px;
            margin: 0 auto;
            cursor: pointer;
            transition: .5s;
            border-radius: 5px;
    }


     .delete-btn:hover {
            background-color: transparent;
            color: var(--primary-color);
        }


</style>