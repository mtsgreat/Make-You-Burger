<template>
   


        <p><Msg :exibirMsg="exibirMsg" v-show="exibirMsg"/></p>
       

        <div>
           <img id="img-teste" src="../../public/img/teste.png" alt="">
            <form id="burger-form" @submit="createdBurger">
                <div class="input-container">
                    <label for="nome">Nome do Cliente:</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome">
                </div>
                <div class="input-container">
                    <label for="pao">Escolha o pão:</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione o seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                    </select>
                   
                </div>
                <div class="input-container">
                    <label for="carne">Escolha a carne:</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">Selecione o tipo de carne</option>
                      <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                    </select>
                   
                </div>
                <div id="opcionais-container" class="input-container">
                    <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
                   <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                       <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                       <span>{{ opcional.tipo }}</span>
                   </div>
                </div>
                
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Montar Hambúrguer">
                </div>
            </form>
        </div>

      

   
</template>


<script>

import Msg from '../components/Msg.vue'

export default {
    name: "BurgerForm",
    data(){
        return {
            paes: null,
            carnes: null,
            opcionaisdata: null,
            nome: null,
            carne: null,
            opcionais: [],
            exibirMsg: null
           
        }
    },
    components: {       
        Msg
    },
    methods: {
        async getIngredientes(){
            //pegando a url
            const req = await fetch("http://localhost:3000/ingredientes");
            //transformando em JSON
            const data = await req.json()

            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
        },
        async createdBurger(e){
            e.preventDefault()

            //objeto com todos os dados do formulario

            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opacionais: Array.from(this.opcionais),
                status: "Solicitado"
            }

            //transformando o objet em texto
            const dataJson = JSON.stringify(data);


            //enviando objeto para o banco

            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: {"Content-Type": "application/json"},
                body: dataJson
            })


            //se quiser ver a resposta
         const res = await req.json(); 
            /* console.log(res);  */

            //exibir msg
          this.exibirMsg = `Seu Pedido de  N°${res.id} foi realizado com sucesso!!`;
         

          setTimeout(() => {
              this.exibirMsg = ""
          },3000) 

            

            //limpar os campos
            this.nome = "",
            this.carne = "",
            this.pao = "",
            this.opcionais = ""
        }
    },
    mounted(){
        this.getIngredientes();
      
    }
}
</script>



<style scoped>
        #burger-form{
            max-width: 400px;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .input-container {
            display: flex;
            flex-direction: column;
            margin-bottom: 20px;
        }

        label{
            font-weight: bold;
            margin-bottom: 15px;
            color: var(--primary-color);
            padding: 4px 10px;
            border-left: 4px solid var(--secundary-color);
        }

        input, select {
            padding: 5px 10px;
            width: 300px;
        }


        #opcionais-container {
            flex-direction: row;
            flex-wrap: wrap;
            flex-direction: row;
            flex-wrap: wrap;
            width: 300px;
        }

        #opcionais-title{
            width: 100%;
        }


        #checkbox-container{
            display: flex;
            align-items: flex-start;
            width: 50%;
            margin-bottom: 20px;
        }


        #opcionais-title {
            width: 100%;
        }


        .checkbox-container {
            display: flex;
            align-items: flex-start;
            width: 50%;
            margin-bottom: 20px;
        }


        .checkbox-container span,
        .checkbox-container input {
            width: auto;
        }

        .checkbox-container span {
            margin-left: 6px;
            font-weight: bold;
        }


        .submit-btn {
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


        .submit-btn:hover {
            background-color: transparent;
            color: var(--primary-color);
        }


        img#img-teste {
        width: 50px;
        position: absolute;
        right: 40px;
        top: 120%;
        opacity: 0;

        
        /* 
        animation: example 10s infinite; */
        }

        @keyframes example {
        0% {width: 50px;  opacity: 0.2;}
        50% {width: 150px; opacity: 0.3;}
        75% {width: 350px; opacity: 1;}
        100% {width: 50px;}
}

</style>