<template>
  <div class="task" :class="stateClass" @click="changeStatus">
      <span @click="deleteTask" class="close">x</span>
      <p>{{ task.name }}</p>
  </div>
</template>

<script>

import EventBus from '@/plugins/EventBus';

export default {
    props: {
        task: { type: Object, required: true }
    },
    computed: {
        stateClass() {
            return this.task.done ? 'done' : 'pending'
        }
    },
    methods: {
        deleteTask() {
            EventBus.sendDeletedTask(this.task.name)
        },
        changeStatus() {
            EventBus.sendTaskStatus(this.task)
        }
    }
}
</script>

<style>
    .task {
        position: relative;
        box-sizing: border-box;
        width: 350px;
        height: 150px;
        padding: 10px;
        border-radius: 8px;
        font-size: 2rem;
        font-weight: 300;
        cursor: pointer;
        user-select: none;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .done {
        color: #DDD;
        border-left: 12px solid #0A8F08;
        background-color: #4ACF50;
        text-decoration: line-through;
    }

    .pending {
        border-left: 12px solid #B73229;
        background-color: #F44336;
    }

    .pending .close {
        background-color: #B73229;
    }

    .done .close {
        background-color: #0A8F08;
    }

    .close {
        position: absolute;
        top: 10px;
        right: 10px;
        font-weight: 600;
        font-size: 0.9rem;
        width: 20px;
        height: 20px;
        border-radius: 50%;
        display: flex;
        justify-content: center;
    }
</style>