<!--ESTRUTURA-->
<template>
    <div class="list row mt-11">
        <div class="col-md-6 listPaciente">
            <h4>Lista de Pacientes</h4>
            <ul class="list-group">
                <li class="list-group-item"
                    :class="{ active: index == currentIndex }"
                    v-for="(paciente, index) in pacientes"
                    :key="index"
                    @click="selecionarPaciente(paciente, index)"
                    >{{ paciente.nome }}</li>
            </ul>
            <button class="m-3 btn btn-danger"
                @click="removerTodosPaciente()">
                Excluir Pacientes
            </button>
        </div>
        <div class="col-md-6 viewPaciente">
            <div v-if="currentPaciente">
                <h4>Paciente</h4>
                    <div>
                        <label>
                            <strong>Nome:</strong>
                        </label>
                        {{ currentPaciente.nome }}
                    </div>
                    <div>
                        <label>
                            <strong>E-mail:</strong>
                        </label>
                        {{ currentPaciente.email }}
                    </div>
                    <div>
                        <label>
                            <strong>Data da Internação:</strong>
                        </label>
                        {{ currentPaciente.data_internacao }}
                    </div>
                    <a class="btn btn-warning"
                        :href="'/pacientes/' + currentPaciente.id">
                    Editar Paciente
                    </a>
            </div>
            <div v-else>
                <h4>Dados do Paciente</h4>
                <p>Por favor, selecione um paciente!</p>
            </div>
        </div>
    </div>
    
</template>

<!--COMPORTAMENTO-->

<script>
import PacienteWS from '../services/PacientesWS';
//import PacientesWS from '../services/PacientesWS';
export default {
    name: "listarPacientes",
    data(){
        return {
            pacientes: [],
            currentIndex: -1,
            currentPaciente: null,
            nome: ""
        };
    },
    methods:{
        obterPacientes(){
            PacienteWS.getPacientes()
                .then(pacientes => {
                    this.pacientes = pacientes.data;
                    console.log(this.pacientes);
                })
                .catch(error => {
                    console.log(error.messege);
                });
        },
        refreshPacientes(){
            this.obterPacientes();
            this.currentPaciente = null;
            this.currentIndex = -1;
        },
        selecionarPaciente(paciente, index){
            this.currentPaciente = paciente;
            this.currentIndex = index;
        },
        removerTodosPaciente(){
            PacienteWS.deletarTodosPacientes()
                .then(res => {
                    console.log(res.data);
                    alert('Todos os Pacientes Excluidos!!');
                    window.location = '/pacientes';
                })
                .catch(error => {
                    console.log(error.messege);
                });
        },
    },
    mounted(){
        this.obterPacientes();
    }
};
</script>

<!--ESTILIZAÇÃO-->
<style>
    .list{
        text-align: left;
        max-width: 750px;
        margin: auto;
        line-height: 5px;
        font-size: 1.0rem;
    }
    .viewPaciente, .listPaciente{
        border:1px solid rgb(172, 169, 169);
        border-radius: 3px;
        padding:10px;
    }   
</style>