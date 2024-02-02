<template>
  <div id="app">
    <MapComponent />
    <FileUploaderComponent />
    <DataFormComponent />
    <UploadToNFTStorage />
  </div>
</template>

<script>
import MapComponent from './components/MapComponent.vue';
import FileUploaderComponent from './components/FileUploaderComponent.vue';
import DataFormComponent from './components/DataFormComponent.vue';
import UploadToNFTStorage from './components/UploadToNFTStorage.vue';

  export default {
    name: 'App',
    components: {
      MapComponent,
      FileUploaderComponent,
      DataFormComponent,
      UploadToNFTStorage
    },
  }


</script>

