<template>
    <div>
        <div class="container-msg">
            <p class="container-msg-success" v-show="textmsgsuccess">{{msg}}</p>
            <p class="container-msg-erro" v-show="textmsgerror">{{msg}}</p>
        </div>
        <form class="form-container" @submit="createBurguer($event)">
            <div>
                <label for="name">Digite o seu nome:</label>
                <input type="text" name="name" class="name" v-model="name"      placeholder="Digite o seu nome">
            </div>
            <div>
                <label for="pao">Escolha o pão:</label>
                <select name="pao" v-model="pao">
                    <option value="" disabled>Selecione o seu pão</option>
                    <option :value="pao.tipo" v-for="pao in paes" :key="pao.id">{{pao.tipo}}</option>
                </select>
            </div>
            <div>
                <label for="carne">Escolha a carne:</label>
                <select name="carne" v-model="carne">
                    <option value="" disabled>Selecione a sua carne</option>
                    <option :value="carne.tipo" v-for="carne in carnes" :key="carne.id">{{carne.tipo}}</option>
                </select>
            </div>
            <div>
                <input class="btn" type="submit" value="Criar meu burguer">
            </div>
        </form>
    </div>
</template>

<script>
export default {
    name: "FormBurguer",
    data(){
        return{
            
            paes: null,
            carnes: null,
            nome: null,
            pao: null,
            carne: null,
            status: "Solicitado",
            msgsucess: null,
            msgerror: null,
            textmsgsuccess: false,
            textmsgerror: false,

        }
    },
    methods: {
        async getIngredients(){
            const req = await fetch("http://localhost:3000/ingredientes")

            const ingredientes = await req.json()
            
            this.paes = ingredientes.paes
            this.carnes = ingredientes.carnes
        },

        async createBurguer(e) {
            e.preventDefault()
            
            const data = {
                name: this.name,
                pao: this.pao,
                carne: this.carne,
                status: "Solicitado"
            }

            console.log(data)

            const dataString = JSON.stringify(data)
            console.log(dataString)

            if(this.name && this.pao && this.carne){
                const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: {"Content-Type" : "application/json"},
                body: dataString
                
            })

                this.msg = "Hamburguer Adicionado com Sucesso"
                this.textmsgsuccess = true
                this.textmsgerror = false
                this.name=""
                this.pao=""
                this.carne=""

            }
            
            else {
                this.msg = "Preencha todos os campos"
                this.textmsgerror = true
                this.textmsgsuccess = false
            }

           
        }
    },
    mounted() {
        this.getIngredients()
    }
}
</script>

<style scoped>
    .form-container{
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        max-width: 500px;
        margin: 0 auto;
        margin-top: 30px;
    }
    .form-container div {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label{
        margin-bottom: 10px;
        font-weight: bold;
        border-left: 3px solid rgb(226, 210, 65);
        padding-left: 10px;
    }

    .name,
    .btn,
    select {
        width: 300px;
        height: 35px;
        padding: 0 10px;
    }

    .btn{
        background-color: rgb(26, 26, 26);
        color: rgb(226, 210, 65);
        border: none;
        font-weight: bold;
        cursor: pointer;
    }

    .opcionais-container{
        display: flex;
        flex-direction: column;
        
    }

    .opcionais-container div {
        display: inline-block
    }
    .opcionais-container div span {
        margin-left: 10px;
    }

    .container-msg{
        display: flex;
        justify-content: center;
    }
    
    .container-msg-success,
    .container-msg-erro{
        text-align: center;
        margin-top: 20px;
        height: 70px;
        width: 300px;
        padding: 20px 20px;
        border: 1px solid green;
        border-radius: 5px;
        background-color: rgb(176, 231, 176);
    }    
    .container-msg-erro{
        border: 1px solid rgb(230, 18, 18);
        background-color: rgb(231, 168, 168);
    }
    
</style>