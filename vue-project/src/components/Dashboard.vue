<template>
    <div class="container">
        <h1>Gerenciar Pedidos</h1>
        <div class="cabecalho">
            <p>#:</p>
            <p class="title">Cliente:</p>
            <p class="title client">Pão:</p>
            <p class="title">Carne:</p>
            <p class="title">Ações:</p>
        </div>
        <div class="list">
            <p class="content" v-for="burguer in burguers" :key="burguer.id">{{burguer.id}}</p>
            <p class="content" v-for="burguer in burguers" :key="burguer.id">{{burguer.name}}</p>
            <p class="content" v-for="burguer in burguers" :key="burguer.id">{{burguer.pao}}</p>
            <p class="content" v-for="burguer in burguers" :key="burguer.id">{{burguer.carne}}</p>
            <div>
                <select name="" id="">
                    <option value="Selecione" v-for="burguer in burguers" :key="burguer.id">{{burguer.status}}</option>
                    <option value="Selecione">Selecione</option>
                </select>
                <button class="btn">Cancelar</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Dashboard",
    data(){
        return {
            id: null,
            name: null,
            pao: null,
            carne: null,
            burguers: null,
        }
    },
    methods: {
        async getData() {
            const req = await fetch("http://localhost:3000/burgers")
            const data = await req.json()
            this.burguers = data
        }
    },
     mounted(){
         this.getData()
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
    }
    .cabecalho,
    .list{
        display: flex;
        margin-bottom: 20px;
        min-width: 700px;
        justify-content: space-between;
        border-bottom: 2px solid black;
        padding-bottom: 10px;
        font-weight: bold;
    }
    .list{
        border-bottom: 1px solid black;
        font-weight: normal;
        min-width: 700px;

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
</style>
