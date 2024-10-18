<template>
  <div class="dashboard">
    <h2>Task Management Dashboard</h2>
    
    <div class="row mb-4">
      <div class="col">
        <b-button @click="showNewTaskModal" variant="primary">Add New Task</b-button>
      </div>
      <div class="col">
        <b-button @click="showNewCategoryModal" variant="secondary">Add New Category</b-button>
      </div>
    </div>

    <h3>Tasks</h3>
    <b-table striped hover :items="tasks" :fields="['title', 'category', 'actions']">
      <template #cell(actions)="data">
        <b-button size="sm" @click="viewTaskDetails(data.item)" class="mr-2">View</b-button>
        <b-button size="sm" @click="editTask(data.item)" variant="warning" class="mr-2">Edit</b-button>
        <b-button size="sm" @click="confirmDeleteTask(data.item)" variant="danger">Delete</b-button>
      </template>
    </b-table>

    <h3>Categories</h3>
    <b-list-group>
      <b-list-group-item v-for="category in categories" :key="category" class="d-flex justify-content-between align-items-center">
        {{ category }}
        <div>
          <b-button size="sm" @click="editCategory(category)" variant="warning" class="mr-2">Edit</b-button>
          <b-button size="sm" @click="confirmDeleteCategory(category)" variant="danger">Delete</b-button>
        </div>
      </b-list-group-item>
    </b-list-group>

    <!-- Task Modal -->
    <b-modal v-model="showTaskModal" :title="isEditingTask ? 'Edit Task' : 'New Task'" @ok="saveTask">
      <b-form>
        <b-form-group label="Title:">
          <b-form-input v-model="currentTask.title" required></b-form-input>
        </b-form-group>
        <b-form-group label="Description:">
          <b-form-textarea v-model="currentTask.description" rows="3"></b-form-textarea>
        </b-form-group>
        <b-form-group label="Category:">
          <b-form-select v-model="currentTask.category" :options="categories"></b-form-select>
        </b-form-group>
      </b-form>
    </b-modal>

    <!-- Category Modal -->
    <b-modal v-model="showCategoryModal" :title="isEditingCategory ? 'Edit Category' : 'New Category'" @ok="saveCategory">
      <b-form>
        <b-form-group label="Category Name:">
          <b-form-input v-model="currentCategory" required></b-form-input>
        </b-form-group>
      </b-form>
    </b-modal>

    <!-- Task Details Modal -->
    <b-modal v-model="showTaskDetailsModal" title="Task Details">
      <p><strong>Title:</strong> {{ currentTask.title }}</p>
      <p><strong>Description:</strong> {{ currentTask.description }}</p>
      <p><strong>Category:</strong> {{ currentTask.category }}</p>
    </b-modal>

    <!-- Confirm Delete Modal -->
    <b-modal v-model="showConfirmModal" title="Confirm Delete" @ok="confirmAction">
      <p>{{ confirmMessage }}</p>
    </b-modal>
  </div>
</template>

<script>
export default {
  name: 'Dashboard',
  data() {
    return {
      tasks: [
        { id: 1, title: 'Task 1', description: 'Description for Task 1', category: 'Work' },
        { id: 2, title: 'Task 2', description: 'Description for Task 2', category: 'Personal' },
      ],
      categories: ['Work', 'Personal', 'Shopping'],
      showTaskModal: false,
      showTaskDetailsModal: false,
      showCategoryModal: false,
      showConfirmModal: false,
      currentTask: {},
      currentCategory: '',
      isEditingTask: false,
      isEditingCategory: false,
      confirmMessage: '',
      confirmAction: null,
    }
  },
  methods: {
    showNewTaskModal() {
      this.isEditingTask = false;
      this.currentTask = { title: '', description: '', category: '' };
      this.showTaskModal = true;
    },
    showNewCategoryModal() {
      this.isEditingCategory = false;
      this.currentCategory = '';
      this.showCategoryModal = true;
    },
    viewTaskDetails(task) {
      this.currentTask = { ...task };
      this.showTaskDetailsModal = true;
    },
    editTask(task) {
      this.isEditingTask = true;
      this.currentTask = { ...task };
      this.showTaskModal = true;
    },
    editCategory(category) {
      this.isEditingCategory = true;
      this.currentCategory = category;
      this.showCategoryModal = true;
    },
    confirmDeleteTask(task) {
      this.confirmMessage = `Are you sure you want to delete the task "${task.title}"?`;
      this.confirmAction = () => this.deleteTask(task);
      this.showConfirmModal = true;
    },
    confirmDeleteCategory(category) {
      this.confirmMessage = `Are you sure you want to delete the category "${category}"?`;
      this.confirmAction = () => this.deleteCategory(category);
      this.showConfirmModal = true;
    },
    saveTask() {
      if (this.isEditingTask) {
        const index = this.tasks.findIndex(t => t.id === this.currentTask.id);
        if (index !== -1) {
          this.tasks.splice(index, 1, this.currentTask);
        }
      } else {
        this.currentTask.id = this.tasks.length + 1;
        this.tasks.push(this.currentTask);
      }
      this.showTaskModal = false;
    },
    saveCategory() {
      if (this.isEditingCategory) {
        const index = this.categories.indexOf(this.currentCategory);
        if (index !== -1) {
          this.categories.splice(index, 1, this.currentCategory);
        }
      } else {
        this.categories.push(this.currentCategory);
      }
      this.showCategoryModal = false;
    },
    deleteTask(task) {
      const index = this.tasks.findIndex(t => t.id === task.id);
      if (index !== -1) {
        this.tasks.splice(index, 1);
      }
    },
    deleteCategory(category) {
      const index = this.categories.indexOf(category);
      if (index !== -1) {
        this.categories.splice(index, 1);
      }
    },
  },
}
</script>

<style scoped>
.dashboard {
  max-width: 800px;
  margin: 0 auto;
}

h2, h3 {
  margin-bottom: 1rem;
}

.mr-2 {
  margin-right: 0.5rem;
}
</style>