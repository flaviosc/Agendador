<template>
    <div id="filtro">
        <br>
        <div class="container">
            <div class="row">
                <div class="col s6">
                    <select class="browser-default" v-model="selecao.unidade" @change="exportaDados">
                        <option value="" disabled>Unidade:</option>
                        <option value="1">Unidade1</option>
                        <option value="2">Unidade2</option>
                        <option value="3">Unidade3</option>
                    </select>
                </div>
                <div class="col s6">
                    <select class="browser-default" v-model="selecao.disciplina" @change="exportaDados">
                        <option value="" disabled>Disciplina:</option>
                        <option value="1234AB">Arquitetura de Computadores</option>
                        <option value="1234CD">Banco de Dados I</option>
                        <option value="1234EF">Matemática Discreta</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="input-field col s12">
                    <label for="data" class="active">Data da Avaliação da Disciplina</label>
                    <input type="date" name='data' class="datepicker" v-model="selecao.data" @change="exportaDados">
                </div>
            </div>
            <div class="row">
                <div class="col s12">
                    <select class="browser-default" v-model="selecao.horario" @change="exportaDados">
                        <option value="" disabled selected>Horário:</option>
                        <option value="horario1">10:00</option>
                        <option value="horario1">14:00</option>
                        <option value="horario1">16:00</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="col s12">
                    <select class="browser-default" v-model="selecao.sala" @change="exportaDados">
                        <option value=""  disabled selected>Sala:</option>
                        <option value="sala1">301</option>
                        <option value="sala2">402</option>
                        <option value="sala3">512</option>
                    </select>
                </div>
            </div>
        </div>
        <br>
    </div>
</template>

<script>
import { Dados } from './Dados.js'
  
export default {
    data() {
        return {
            selecao: {
                disciplina: '',
                unidade: '',
                data: '',
                hora: '',
                sala: ''
            },
        };
    },
    methods: {
        exportaDados() {
            Dados.$emit('selecao',this.selecao);
        },
    },
    mounted: function(){
        var diaSemana = [ 'Domingo', 'Segunda-Feira', 'Terca-Feira', 'Quarta-Feira', 'Quinta-Feira', 'Sexta-Feira', 'Sabado' ];
        var mesAno = [ 'Janeiro', 'Fevereiro', 'Marco', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro'           , 'Dezembro' ];
        var data = new Date();
        var hoje = diaSemana[data.getDay()] + ', ' + mesAno[data.getMonth()] + ' de ' + data.getFullYear();
        $("#dataPesquisa").attr("value", hoje);
        $(".datepicker").pickadate({
            monthsFull: mesAno,
            monthsShort: [ 'Jan', 'Fev', 'Mar', 'Abr', 'Mai', 'Jun', 'Jul', 'Ago', 'Set', 'Out', 'Nov', 'Dez' ],
            weekdaysFull: diaSemana,
            weekdaysShort: [ 'Dom', 'Seg', 'Ter', 'Qua', 'Qui', 'Sex', 'Sab' ],
            weekdaysLetter: [ 'D', 'S', 'T', 'Q', 'Q', 'S', 'S' ],
            selectMonths: true,
            selectYears: true,
            clear: false,
            format: 'dddd/mm/yyyy',
            today: "Hoje",
            close: "X",
            min: new Date(data.getFullYear() - 1, 0, 1),
            max: new Date(data.getFullYear() + 1, 11, 31),
            closeOnSelect: true
        });

        $("#dataPesquisa").click(function (event) {
            event.stopPropagation();
            $(".datepicker").first().pickadate("picker").open();
        });

        }
    }
</script>

<style>
</style>
