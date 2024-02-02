<template>
  <div>
    <input type="file" @change="handleFileChange" accept="image/*">
    <button @click="uploadToNFTStorage">Upload to NFT.storage</button>
    <div v-if="uploadUrl">Uploaded: <a :href="uploadUrl" target="_blank">{{ uploadUrl }}</a></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      file: null,
      uploadUrl: '',
    };
  },
  methods: {
    handleFileChange(event) {
      this.file = event.target.files[0];
    },
    async uploadToNFTStorage() {
      if (!this.file) return;

      try {
        const formData = new FormData();
        formData.append('file', this.file);

        const response = await fetch('https://api.nft.storage/upload', {
          method: 'POST',
          headers: {
            // Replace 'your_api_key' with your actual NFT.storage API key
            'Authorization': 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJkaWQ6ZXRocjoweDZhRmQ5M0JiNzQwM2RlQ2Y4NGVmRWRCRjlBNUFkNWM5RUQ1YjhFRjQiLCJpc3MiOiJuZnQtc3RvcmFnZSIsImlhdCI6MTY0NzU1NTQ4NTA4MSwibmFtZSI6Inlvb2NhdHMifQ.aZot4G1rrH-ED9tXIV9VAa3OCS87g6nBQEM1paBiIxI',
          },
          body: formData,
        });

        if (!response.ok) {
          throw new Error(`Upload failed: ${response.statusText}`);
        }

        const data = await response.json();
        this.uploadUrl = `https://ipfs.io/ipfs/${data.value.cid}`;
      } catch (error) {
        console.error('Upload error:', error);
      }
    },
  },
};
</script>

