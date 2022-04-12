<template>
  <q-page class="bg-grey-3 column">
    <div class="q-pa-sm">
      <q-input v-model="novaTarefa" class="col" @keyup.enter="adicionarTarefa">
      </q-input>
    </div>
    <q-list class="bg-white q-mx-sm" separator bordered>

      <q-item
        v-for="(tarefa, index) in tarefas"
        :key="tarefa.nome"
        clickable
        @click="tarefa.feito = !tarefa.feito"
        :class="{'bg-blue-1':tarefa.feito}"
        v-ripple>
        <q-item-section avatar>
          <q-checkbox v-model="tarefa.feito" color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ tarefa.nome }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="tarefa.feito" side>
          <q-btn @click.stop="apagarTarefa(index)" flat round color="primary" icon="delete" />
        </q-item-section>
      </q-item>

    </q-list>
  </q-page>
</template>

<script>

export default {
  data() {
    return {
      novaTarefa: "",
      tarefas: [
        {
          nome: "Acordar",
          feito: false
        },
        {
          nome: "Tomar café",
          feito: false
        },
        {
          nome: "Trabalhar",
          feito: false
        }
      ]
    }
  },
  methods: {
    apagarTarefa(index) {
      this.$q.dialog({
        title: 'Alerta',
        message: 'Deseja mesmo apagar a tarefa da lista?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tarefas.splice(index, 1)
        this.$q.notify({
          type: 'positive',
          message: 'Tarefa excluída com sucesso!'
        })
      })
    },
    adicionarTarefa() {
      this.tarefas.push({
        nome: this.novaTarefa,
        feito: false
      })
      this.novaTarefa = ""
    }
  }
}
</script>
