<template>
    <div>
        <Message :msg="msg" v-show="msg" />
        <div>
            <form id="burger-form" @submit="createBurger">
                <div class="input-container">
                    <label for="nome"> Nome do Cliente: </label>
                    <input type="text" id="nome" v-model="nome" placeholder="Digite o seu nome">
                </div>

                <div class="input-container">
                    <label for="pao">Escolha do pão:</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione o seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                    </select>
                </div>

                <div class="input-container">
                    <label for="carne">Escolha a carne do seu Burger:</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">Selecione o tipo de carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{carne.tipo}}</option>
                    </select>
                </div>

                <div class="input-container" id="opcionais-container">
                    <label for="opcinais" id="opcionais-title">Selecione os opcionais:</label>
                    <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                        <span>{{ opcional.tipo }}</span>
                    </div>
                    
                </div>

                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar meu Burger!">
                </div>
            </form>
        </div>
    </div>
</template>
<script>
import { defineComponent } from 'vue';
import Message from './Message.vue';


export default defineComponent({
    name: 'Burgerform',
    components: {
        Message
    },
    data () {
        return{
          //dados que vem do servidor
          paes: null,
          carnes: null,
          opcionaisdata: null,

          //dados que são enviados
          nome: null,
          pao: null,
          carne: null,

          opcionais:[],
          msg:null

        }
    },

    methods: {
        async getIngredientes(){
            const req = await fetch("https://makeyourburgerapi.herokuapp.com/ingredientes");
            const data = await req.json();
            
            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;            
        },
        async createBurger(e){
            e.preventDefault();
            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais),
                status:"Solicitado",
                msg: null
            }
            const dataJson = JSON.stringify(data);
            const req = await fetch('https://makeyourburgerapi.herokuapp.com/burgers',{
                method: "POST",
                headers:{
                    "Content-Type": "application/json"
                },
                body: dataJson
            });
            const res = await req.json();
            console.log(res);

            //colocar mensagem no sistema
            this.msg = `Pedido Nº ${res.id} realizado com sucesso!`;

            //limpar mensagem
            setTimeout(() => {this.msg=""}, 5000);

            //limpar campos
            this.nome = "";
            this.pao = "" ;
            this.carne = "";
            this.opcionais = ""; 

        }
    },
    mounted(){
        this.getIngredientes();
    
    }  

})   
</script>

<style scoped>
    #burger-form {
        max-width: 300px;
        margin: 0 auto;
    }
    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }
    label{
        font-weight: bold;
        margin-bottom:15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #fcba03;
    }
    input, select {
        padding: 5px 10px;
        width: 300px;
    }
    #opcionais-container{
        flex-direction: row;
        flex-wrap: wrap;
    }
    #opcionais-title{
        width: 100%
    }
    .checkbox-container{
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }
    .checkbox-container span,
    .checkbox-container input{
        width: auto;
    }   

    .checkbox-container span{
        margin-left: 6px;
        font-weight: bold;
    }
    .submit-btn{
       background-color: #222;
       color: #fcba03;
       font-weight: bold;
       border: 2px solid #222;
       padding: 10px;
       font-size: 16px;
       cursor: pointer;
       transition: .5s;
    }
    .submit-btn:hover{
        background-color: transparent;
        color: #222;
    }

</style>