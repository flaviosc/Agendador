<template>
    <div class="container">
        <div>
            <p id="textoAjuda" class="center-align">Clique numa disciplina abaixo para começar a agendar</p>
        </div>
        <div>
            <disciplina v-for="disciplina in disciplinas" :disciplina.sync="disciplina" :key="disciplina.codigo"></disciplina>
        </div>
        <div class="row center">
            <a class="red darken-4 waves-light btn" onclick="window.print();">Imprimir Comprovante</a>
        </div>
    </div>
</template>

<script>
    import sweetalert from 'sweetalert';
    import Disciplina from './Disciplina';
    export default {
        props:['disciplinas'],
        components: {
            Disciplina,
        },
    };
</script>
