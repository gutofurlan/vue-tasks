<template>
    <div>
        <h1>{{title}}</h1>
        
        <form class="form form-inline">
            <input type="text" placeholder="Encontrar?" class="form-control" v-model="filter">
        </form>
        <br/>
        <form class="form form-inline" @submit.prevent="onSubmit">
            <input type="text" placeholder="Nome da tarefa" class="form-control" v-model="task.name">
            <button type="submit" class="btn btn-primary">Cadastrar</button>
        </form>
        <br/>
        <table class="table table-dark">
            <thead>
                <tr>
                    <td>Id.</td>
                    <td>Nome</td>
                    <td width="150px">Ações</td>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(t, index) in filteredItems" :key="index">
                    <td>{{ t.id }}</td>
                    <td>{{ t.name }}</td>
                    <td width="150px">
                        <a href="#" class="btn btn-info" @click.prevent="edit(t.id)">Editar</a>
                        <a href="#" @click.prevent="deleteTask(t.id)" class="btn btn-danger">Deletar</a>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>

export default {
    data () {
        return {
            title: 'Lista de tarefas',
            tasks: [],
            task: {id:'', name: ''},
            updating: false,
            updateIndice: '',
            filter: ''
        }
    }, methods : {
        onSubmit() {
            if(!this.updating) {
                return this.save();
            } else {
                return this.update();
            }
        },
        save () {
            let idTask = this.tasks.length + 1
            this.task.id = idTask
            this.tasks.push(this.task)
            this.clearForm()
        },
        edit(id) {
            alert(id)
            this.updateIndice = this.findIndexItem(id)
            this.task = this.tasks[this.updateIndice]
            this.updating = true
        }, 
        update() {
            this.tasks[this.updateIndice] = this.task
            this.clearForm()
            this.updating = false
        }, 
        clearForm() {
            this.task = {id: '', name: ''}
        }, 
        deleteTask(id) {
            this.tasks.splice(this.findIndexItem(id), 1) // remove do array
        },
        findIndexItem() {
            for (let index = 0; index < this.tasks.length; index++) {
                if(this.tasks[index].id == id) {
                    return index
                }
                
            }
        }
    },
    computed: {
        filteredItems () {
            if (this.filter === '') 
                return this.tasks

            let vm = this
            return this.tasks.filter( function (task) {
                return task.name.indexOf(vm.filter) > -1 //se n encontra retorna -1
            })
            // return this.tasks.filter( function (task) {
            //     return task['name'].includes(vm.filter) 
            // })
        }   
    }
}
</script>


<style scoped>

</style>
