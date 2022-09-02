<template>
    <div class="container">
        <h1>Gerenciar Pedidos</h1>
        <div class="container-msg" v-show="textmsg">
            <p class="msg">{{msg}}</p>
        </div>
        <div class="cabecalho">
            <p>#:</p>
            <p class="title">Cliente:</p>
            <p class="title client">Pão:</p>
            <p class="title">Carne:</p>
            <p class="title">Ações:</p>
        </div>
        <div class="list" v-for="burguer in burguers" :key="burguer.id">
            <p class="content">{{burguer.id}}</p>
            <p class="content">{{burguer.name}}</p>
            <p class="content">{{burguer.pao}}</p>
            <p class="content">{{burguer.carne}}</p>
            <div>
                <select name="select" @change="burguerUpdate($event, burguer.id)">
                    <option value="">Selecione</option>
                    <option v-for="status in status" :key="status.id" :value="status.tipo" :selected="status.tipo === burguer.status">{{status.tipo}}</option>
                </select>
                <button @click="deleteBurguer(burguer.id)" class="btn">Cancelar</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Dashboard",
    data(){
        return {
            burguers: null,
            status: null,
            msg: null,
            textmsg: false
            
        }
    },
    methods: {
        async getData() {
            const req = await fetch("http://localhost:3000/burgers")
            const data = await req.json()
            this.burguers = data
        },

        async getStatus() {
            const req = await fetch("http://localhost:3000/status")
            const status = await req.json()
            this.status = status
        },
        
        async deleteBurguer(id){
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "DELETE",
            })

            const req2 = await fetch("http://localhost:3000/burgers") 
            const data = await req2.json()
            this.burguers = data
        },

        async burguerUpdate(e, id) {
            const option = e.target.value
            const dataJson = JSON.stringify({ status: option })

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "PATCH",
                headers: {
                    "Content-Type" : "application/json"
                },
                body: dataJson
            })

            const res = await req.json()

            this.msg = `O pedido n: ${res.id} está ${res.status}`
            this.textmsg = true
            
            

        },
        
    },

     mounted(){
         this.getData()
         this.getStatus()
     }
}
</script>

<style>
    .container{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    h1{
        margin: 50px 0;
        margin-bottom: 15px;
    }
    .cabecalho,
    .list{
        display: flex;
        margin-bottom: 20px;
        min-width: 900px;
        justify-content: space-between;
        border-bottom: 2px solid black;
        padding-bottom: 10px;
        font-weight: bold;
    }
    .list{
        border-bottom: 1px solid black;
        font-weight: normal;
        min-width: 900px;

    }
    .title{
        width: 120px;
    }

    .btn{
        padding: 10px;
        margin-left: 10px;
        background-color: rgb(26, 26, 26);
        color: rgb(226, 210, 65);
        border: none;
        font-weight: bold;
        cursor: pointer;
    }

    select{
        padding: 9px
    }

    .container-msg{
        display: flex;
        justify-content: center;
        margin-bottom: 40px;
    }
    
    .msg{
        text-align: center;
        margin-top: 20px;
        height: 70px;
        width: 300px;
        padding: 20px 20px;
        border: 1px solid rgb(37, 186, 197);
        border-radius: 5px;
        background-color: rgb(145, 215, 233);
    }    
</style>
