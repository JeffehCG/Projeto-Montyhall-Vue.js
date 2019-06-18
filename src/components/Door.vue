<template>
    <div class="door-area">
        <div class="door-frame" :class="{selected: selected && !open}"> <!--Aplica a classe selected se a variavel estiver selected estiver true, e open false -->
                <Gift v-if="hasGift && open"/> <!--Se as duas variaveis forem verdadeiras exibir presente-->
        </div>
        <div class="door" :class="{open}"
            @click="selected = !selected"> <!--Clicando na posta , selected vai ser igual ao oposto, ou seja, se for falso sera true-->
            <div class="number" :class="{selected}">{{number}}</div> <!--Numero passado por parametro-->
            <div class="knob" :class="{selected}"
                @click.stop="open = true"></div> <!--Maçaneta da porta-->
        </div>
    </div>
</template>

<script>
import Gift from './Gift'

export default {
    name: 'Door',
    components: {Gift},
    props: { //Propriedades passadas por parametro
        number: {},
        hasGift: {type: Boolean}
    },
    data: function(){ //Atributos do objeto (Cada vez que o componente for chamado, istanciara objetos)
        return{
            open: false, //Identificando se a porta esta aberta
            selected: false //Identificando se a porta esta selecionada
        }
    }

}
</script>

<style>
:root{ /*Variaveis CSS*/
    --door-border: 5px solid brown;
    --selected-border: 5px solid yellow;
}

.door-area{
    position: relative;
    width: 200px;
    height: 310px;
    border-bottom: 10px solid #aaa;
    margin-bottom: 20px;
    font-size: 3rem;

    display: flex;
    justify-content: center;
}

.door-frame{
    position: absolute;
    height: 300px;
    width: 180px;

    border-left: var(--door-border);
    border-top: var(--door-border);
    border-right: var(--door-border);

    display: flex;
    justify-content: center;
    align-items: flex-end;
}

.door{
    position: absolute;
    top: 5px;
    height: 295px;
    width: 170px;
    background-color: chocolate;

    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
}

.door .knob{
    height: 20px;
    width: 20px;
    border-radius: 10px;
    background-color: brown;
    align-self: flex-start;
    margin-top: 60px;
}

.door-frame.selected{
    border-left: var(--selected-border);
    border-top: var(--selected-border);
    border-right: var(--selected-border);
}

.door .number.selected {
    color: yellow;
}

.door .knob.selected{
    background-color: yellow;
}

.door.open{
    background-color: #0007;
}

.door.open .knob{
    display: none;
}

.door.open .number{
    display: none;
}

</style>
