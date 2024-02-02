<template>
  <div>
    <input type="file" @change="handleFileChange" accept="image/*" class="mb-2 p-2 border rounded-md">
    <button @click="uploadImage" class="bg-blue-500 text-white p-2 rounded-md hover:bg-blue-600">Upload Image</button>
    <div v-if="imageUrl" class="mt-4">
      <img :src="imageUrl" alt="Uploaded Image" class="border rounded-md" style="max-width: 100%;">
    </div>
  </div>
</template>

<script>
export default {
  name: 'FileUploaderComponent',
  data() {
    return {
      file: null,
      imageUrl: null,
    };
  },
  methods: {
    handleFileChange(event) {
      this.file = event.target.files[0];
      this.createImageURL();
    },
    uploadImage() {
      // Implement the upload logic here
      // For demonstration, we'll just log the file name
      console.log(`Uploading ${this.file.name}...`);
      // After successful upload, you might want to reset the file and imageUrl
      // this.file = null;
      // this.imageUrl = null;
    },
    createImageURL() {
      if (this.file) {
        this.imageUrl = URL.createObjectURL(this.file);
      }
    }
  }
}
</script>

<style scoped>
/* Add styles if needed */
</style>

