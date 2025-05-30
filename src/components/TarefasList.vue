<template>
    <div class="task-list-container">
        <h1 class="task-list-title">Lista de Tarefas</h1>
        
        <!-- Filtros -->
        <div class="filters-container">
            <div class="filters">
                <button 
                    v-for="filter in filters" 
                    :key="filter.value"
                    @click="currentFilter = filter.value"
                    :class="['filter-button', { active: currentFilter === filter.value }]"
                >
                    {{ filter.label }}
                </button>
            </div>
        </div>

        <!-- Formulário de nova tarefa -->
        <form @submit.prevent="addTask" class="task-form">
            <div class="form-group">
                <input 
                    v-model="newTask.title"
                    type="text"
                    placeholder="Nova tarefa"
                    class="task-input"
                    required
                />
                <button 
                    type="submit"
                    class="add-button"
                >
                    Adicionar
                </button>
            </div>
        </form>

        <!-- Lista de tarefas -->
        <ul class="tasks-list">
            <li 
                v-for="task in filteredTasks" 
                :key="task.id"
                class="task-item"
            >
                <div class="task-content">
                    <input 
                        type="checkbox"
                        :checked="task.completed"
                        @change="toggleTask(task)"
                        class="task-checkbox"
                    />
                    <span :class="{ completed: task.completed }">
                        {{ task.title }}
                    </span>
                </div>
                <button 
                    @click="removeTask(task)"
                    class="remove-button"
                >
                    Remover
                </button>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    data() {
        return {
            tasks: [
                { id: 1, title: 'Estudar Vue.js', completed: false },
                { id: 2, title: 'Fazer exercícios', completed: true },
                { id: 3, title: 'Ler um livro', completed: false }
            ],
            newTask: { title: '' },
            currentFilter: 'all',
            filters: [
                { label: 'Todas', value: 'all' },
                { label: 'Pendentes', value: 'pending' },
                { label: 'Concluídas', value: 'completed' }
            ]
        }
    },
    computed: {
        filteredTasks() {
            switch (this.currentFilter) {
                case 'completed':
                    return this.tasks.filter(task => task.completed)
                case 'pending':
                    return this.tasks.filter(task => !task.completed)
                default:
                    return this.tasks
            }
        }
    },
    methods: {
        addTask() {
            if (this.newTask.title.trim()) {
                this.tasks.unshift({
                    id: Date.now(),
                    title: this.newTask.title,
                    completed: false
                })
                this.newTask.title = ''
            }
        },
        toggleTask(task) {
            task.completed = !task.completed
        },
        removeTask(task) {
            const index = this.tasks.indexOf(task)
            if (index > -1) {
                this.tasks.splice(index, 1)
            }
        }
    }
}
</script>

<style scoped>
.task-list-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 1rem;
}

.task-list-title {
    font-size: 1.5rem;
    font-weight: bold;
    margin-bottom: 1.5rem;
}

.filters-container {
    margin-bottom: 1.5rem;
}

.filters {
    display: flex;
    gap: 0.5rem;
}

.filter-button {
    padding: 0.5rem 1rem;
    border-radius: 0.375rem;
    background-color: #e5e7eb;
    border: none;
    cursor: pointer;
    transition: background-color 0.2s;
}

.filter-button:hover {
    background-color: #d1d5db;
}

.filter-button.active {
    background-color: #3b82f6;
    color: white;
}

.task-form {
    margin-bottom: 1.5rem;
}

.form-group {
    display: flex;
    gap: 0.5rem;
}

.task-input {
    flex: 1;
    padding: 0.5rem 1rem;
    border: 1px solid #d1d5db;
    border-radius: 0.375rem;
}

.add-button {
    padding: 0.5rem 1rem;
    background-color: #22c55e;
    color: white;
    border: none;
    border-radius: 0.375rem;
    cursor: pointer;
    transition: background-color 0.2s;
}

.add-button:hover {
    background-color: #16a34a;
}

.tasks-list {
    list-style: none;
    padding: 0;
    margin: 0;
}

.task-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
    background-color: white;
    border-radius: 0.5rem;
    margin-bottom: 0.5rem;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.task-content {
    display: flex;
    align-items: center;
    gap: 0.75rem;
}

.task-checkbox {
    width: 1.25rem;
    height: 1.25rem;
}

.completed {
    text-decoration: line-through;
    color: #6b7280;
}

.remove-button {
    color: #ef4444;
    background: none;
    border: none;
    cursor: pointer;
    padding: 0.25rem;
}

.remove-button:hover {
    color: #dc2626;
}

@media (max-width: 640px) {
    .task-list-container {
        padding: 0.5rem;
    }

    .form-group {
        flex-direction: column;
    }

    .add-button {
        width: 100%;
    }
}
</style>