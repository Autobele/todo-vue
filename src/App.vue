<template>
	<div id="app">
		<h1>ToDo</h1>
		<TaskProgress :progress="progress"/>
		<NewTask @taskAdded="addTask"/>
		<TaskGrid 
		:tasks="tasks"/>
	</div>
</template>

<script>

import TaskGrid from '@/components/TaskGrid.vue';
import NewTask from '@/components/NewTask.vue';
import EventBus from '@/plugins/EventBus';
import TaskProgress from '@/components/TaskProgress.vue';

export default {
	components: { TaskGrid, NewTask, TaskProgress },
	data() {
		return {
			tasks: []
		}
	},
	computed: {
		progress() {
			const total = this.tasks.length;
			const done = this.tasks.filter(t => t.done).length
			return Math.round(done / total * 100) || 0
		}
	}
	,
	methods: {
		addTask(task) {
			const sameName = t => (t.name).toLowerCase() == task.name.toLowerCase()
			const reallyNew = this.tasks.filter(sameName).length == 0
			if(reallyNew) {
				this.tasks.push({
					name: task.name,
					done: false
				})
			}
		},
	},
	created() {
		EventBus.receiveDeletedTask( name => {
			const position = this.tasks.map(task => task.name).indexOf(name)
			this.tasks.splice(position, 1)
		})

		EventBus.reciveTaskStatus( task => { task.done = !task.done})

		const json = localStorage.getItem('tasks')
		const array = JSON.parse(json)
		this.tasks = Array.isArray(array) ? array : []
	},
	watch: {
		tasks: {
			deep: true,
			handler() {
				localStorage.setItem('tasks', JSON.stringify(this.tasks))
			}
		}
	}
}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
</style>
