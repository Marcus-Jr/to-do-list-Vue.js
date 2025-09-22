<template>
  <section>
    <div class="panel">
      <form class="form" @submit.prevent="addTask">
        <div class="form-header">
          <p>To Do List</p>
        </div>
        
        <div class="form-group">
          <label class="form-label">Tarefa</label>
          <input 
            type="text" 
            class="form-input" 
            placeholder="Digite uma tarefa..."
          >
        </div>
        
        <button type="submit" class="btn" :disabled="!formValid">
          Adicionar
        </button>
      </form>
    </div>

    <section>
    </section>
  </section>
</template>

<script>
export default {
  name: 'FormTask',

  data() {
    return {
      formValues: {
        task: ''
      }
    };
  },
  methods: {
    setJSON(tasks) {
      localStorage.setItem('dataJson', JSON.stringify(tasks));
    },

    getJSON() {        
      const dataSavedJson = localStorage.getItem('dataJson');
      return dataSavedJson ? JSON.parse(dataSavedJson) : [];  
    },

    addTask() {
      let tasks = this.getJSON();
      const newTask = {
        id: Date.now(),
        task: this.formValues.task,
      };
      tasks.push(newTask);
      this.setJSON(tasks);
      this.list = this.getJSON();
      this.formValues.task = '';
    },
  },
  computed: {
    formValid() {
      return this.formValues.task.trim().length > 0;
    }
  }

}
</script>

<style>
body {
  background-color: #094067;
}

.panel {
  max-width: 450px;
  margin: 40px auto;
  background: #fff;
  padding: 25px 30px;
  border-radius: 12px;
  box-shadow: 15px 6px 15px rgba(0, 0, 0, 0.15);
}

.form-header p {
  font-size: 22px;
  font-weight: bold;
  color: #094067;
  text-align: center;
  margin-bottom: 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
  margin-bottom: 18px;
}

.form-label {
  margin-bottom: 6px;
  font-size: 14px;
  font-weight: 600;
  color: #5f6c7b;
}

.form-input {
  padding: 10px 14px;
  border: 2px solid #3da9fc;
  border-radius: 8px;
  font-size: 15px;
  outline: none;
  transition: 0.3s;
}

.form-input:focus {
  border-color: #094067;
  box-shadow: 0 0 6px rgba(61, 169, 252, 0.5);
}

.btn {
  width: 100%;
  padding: 10px 14px;
  border: none;
  border-radius: 8px;
  background-color: #3da9fc;
  color: #fff;
  font-size: 16px;
  font-weight: bold;
  transition: background 0.3s;
  cursor: pointer;
}

.btn:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}

.btn:not(:disabled):hover {
  background-color: #094067;
}
</style>