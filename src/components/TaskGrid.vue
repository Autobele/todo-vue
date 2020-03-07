<template>
    <div class="task-grid">
        <template v-if="tasks.length">
            <Task v-for="(task) in tasks" :key="task.name"
            :task="task"
            />
        </template>
        <p v-else class="no-task">Sua vida está em dia :)</p>
    </div>
</template>

<script>
import Task from '@/components/Task.vue';

export default {
    components: { Task },
    props: {
        tasks: { type: Array, required: true}
    },
    methods: {
        
    }
}
</script>

<style>
    .task-grid {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
    }

    .task-grid .task {
        margin: 10px;
    }

    .no-task {
        font-size: 1.7rem;
        color: #AAA;
    }
</style>