<template>
  <div class="new-task">
      <input type="text" v-model="name" @keydown.enter="add"
      class="form-element" placeholder="Whats ur plan Batman?">
      <button class="btnAdd">+</button>
  </div>
</template>

<script>
export default {
    data() {
        return {
            name: ''
        }
    },
    methods: {
        add() {
            this.$emit('taskAdded', {name: this.name})
            this.name = ''
        }
    }
}
</script>

<style>
    *{
        box-sizing: border-box;
    }
    .new-task {
        width: 100%;
        display: flex;
        margin: 20px;
    }
    .form-element {
        flex: 1;
        height: 50px;
        text-indent: 15px;
        font-size: 18px;
        border-radius: 5px 0 0 5px;
        border: none;
    }
    .new-task .btnAdd {
        width: 50px;
        font-size: 22px;
        background-color: #FFCE00;
        color: #FFF;

        border: none;
        border-radius: 0px 5px 5px 0px;
        outline: none;
        cursor: pointer;

        transition: 0.2s background-color ease-out;
    }

    .new-task .btnAdd:hover {
        background-color: #FFAA20;
    }
</style>