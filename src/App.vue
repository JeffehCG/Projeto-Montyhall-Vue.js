<template>
    <div id="app">
        <h1>Problema de Monty Hall</h1>
        <!--Formulario de opções do Monty Hall-->
        <div class="form">
            <div v-if="!started"> <!--Exibir conteudo apenas se não estiver startado-->
                <label for="portsAmount">Quantas portas?</label>
                <input type="text" id="portsAmount" size="3"
                    v-model.number="portsAmount"> <!--v-model = salva automaticamente o que esta no input /.number = salvar como numero-->
            </div>
            <div v-if="!started">
                <label for="selectedPort">Qual porta é premiada?</label>
                <input type="text" id="selectedPort" size="3"
                    v-model.number="selectedPort">
            </div>
            <button v-if="!started" @click="started = true">Iniciar</button>
            <button v-if="started" @click="started = false">Reiniciar</button>
        </div>

        <!-- Exibição das portas, de acordo com o formulario -->
        <div class="doors" v-if="started"> <!--Só vai aparecer quando estiver startado-->
            <div v-for="i in portsAmount" :key="i"> <!--Criando a quantidade de portas selecionada-->
                <Door :hasGift = " i == selectedPort" :number = "i" /> <!--Chamando a porta / se o indice for igual ao numero selecionado da porta primiada, hasGift sera true, e sera passado como propriedade para o componente door-->
            </div>
        </div>
    </div>
</template>

<script>
import Door from './components/Door'

export default {
    name: 'App', //nome do componente 
    components: {Door}, //Referenciando componentes importados
    data: function(){ //Atributos do objeto
        return{
            started: false,
            portsAmount: 3, //Quantidades de portas (por padrão 3)
            selectedPort: null
        }
    }
}
</script>

<style>
*{
    box-sizing: border-box;
    font-family: 'Montserrat', 'sans-serif'
}

body{
    color: #fff;
    background: linear-gradient(to right, rgb(21,153,87), rgb(21,87,153));
}

#app{
    display: flex;
    flex-direction: column;
    align-items: center;
}

#app h1 {
    border: 1px solid #000;
    background-color: #0004;
    padding: 20px;
    margin-bottom: 60px;
}

.form{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-bottom:40px; 
}

.form, .form input, .form button{
    margin: 10px;
    font-size: 2rem;
}

.doors {
    align-self: stretch;
    display: flex;
    justify-content: space-around;

    flex-wrap: wrap; /*Quando diminuir a tela, quebrar a linha e colocar as postas para baixo*/
}
</style>
