<template>
    <form>
        <div>
            <label for="name">Digite o seu nome:</label>
            <input type="text" name="name" class="name" v-model="name" placeholder="Digite o seu nome">
        </div>
        <div>
            <label for="pao">Escolha o pão:</label>
            <select name="pap" v-model="pao">
                <option value="">Selecione o seu pão</option>
                <option value="integral">Integral</option>
            </select>
        </div>
        <div>
            <label for="carne">Escolha a carne:</label>
            <select name="carne" v-model="carne">
                <option value="">Selecione a sua carne</option>
                <option value="maminha">Maminha</option>
            </select>
        </div>
        <div>
            <label for="opcionais">Opcionais:</label>
            <input type="checkbox" name="opcionais" v-model="opcionais" value="salame">
            <span>Salame</span>
        </div>
        <div>
            <input type="submit" value="Criar meu burguer">
        </div>
    </form>
</template>

<script>
export default {
    name: "FormBurguer"
}
</script>