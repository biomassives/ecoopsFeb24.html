<template>
  <form @submit.prevent="submitData">
    <div class="form-group">
      <label for="coordinates">Coordinates</label>
      <input type="text" id="coordinates" v-model="formData.coordinates" class="input" placeholder="Latitude, Longitude" required>
    </div>
    <div class="form-group">
      <label for="description">Description</label>
      <textarea id="description" v-model="formData.description" class="textarea" placeholder="Enter a description..." required></textarea>
    </div>
    <button type="submit" class="btn-submit">Submit</button>
  </form>
</template>

<script>
export default {
  name: 'DataFormComponent',
  data() {
    return {
      formData: {
        coordinates: '',
        description: ''
      }
    };
  },
  methods: {
    submitData() {
      console.log('Form Data:', this.formData);
      // Reset form after submission
      this.formData.coordinates = '';
      this.formData.description = '';
    }
  }
}
</script>

<style scoped>
.form-group {
  margin-bottom: 1rem;
}

.input, .textarea {
  width: 100%;
  padding: 0.5rem;
  margin-top: 0.25rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.btn-submit {
  background-color: #3498db;
  color: white;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn-submit:hover {
  background-color: #2980b9;
}
</style>

