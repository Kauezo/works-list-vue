<template>
    <div class="app-container">
        <div class="app-content">
            <tarefas-list></tarefas-list>
        </div>
    </div>
</template>


<script>
import TarefasList from './components/TarefasList.vue'

export default {
    components: { TarefasList }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background-color: #f3f4f6;
    line-height: 1.6;
    color: #333;
}

.app-container {
    min-height: 100vh;
    background-color: #f3f4f6;
}

.app-content {
    padding: 2rem 1rem;
    max-width: 1200px;
    margin: 0 auto;
}
</style>
