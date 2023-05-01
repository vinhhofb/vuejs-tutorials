<template>
  <div class="card">
    <div class="top">
      <p>Drag & drop image uploading</p>
      
    </div>
    <div class="drag-area" @dragover.prevent="onDragOver" @dragleave.prevent="onDragLeave" @drop.prevent="onDrop">
      <span v-if="!isDragging">
        Drag & drop image here or
        <span class="select" role="button" @click="selectFiles">Browse</span>
      </span>
      <span v-else class="select">Drop images here</span>
      <input name="file" type="file" class="file" ref="fileInput" @change="onFileSelect" multiple />
    </div>

    <!-- IMAGE PREVIEW CONTAINER -->
    <div class="container">
      <div class="image" v-for="(image, index) in images" :key="index">
        <span class="delete" @click="deleteImage(index)">&times;</span>
        <img :src="image.url" />
      </div>
    </div>
    <button type="button" @click="uploadImages">Upload</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      images: [],
      isDragging: false,
    };
  },
  methods: {
    selectFiles() {
      this.$refs.fileInput.click();
    },
    onFileSelect(event) {
      const files = event.target.files;
      if (files.length === 0) return;

      for (let i = 0; i < files.length; i++) {
        if (files[i].type.split("/")[0] !== "image") continue;
        if (!this.images.some((e) => e.name === files[i].name)) {
          this.images.push({ name: files[i].name, url: URL.createObjectURL(files[i]) });
        }
      }
    },
    deleteImage(index) {
      this.images.splice(index, 1);
    },
    onDragOver(event) {
      event.preventDefault();
      this.isDragging = true;
      event.dataTransfer.dropEffect = "copy";
    },
    onDragLeave(event) {
      event.preventDefault();
      this.isDragging = false;
    },
    onDrop(event) {
      event.preventDefault();
      this.isDragging = false;
      const files = event.dataTransfer.files;
      for (let i = 0; i < files.length; i++) {
        if (files[i].type.split("/")[0] !== "image") continue;
        if (!this.images.some((e) => e.name === files[i].name)) {
          this.images.push({ name: files[i].name, url: URL.createObjectURL(files[i]) });
        }
      }
    },
    uploadImages() {
      console.log("Uploading images:", this.images);
    },
  },
};
</script>

<style>
.card {
    width: 100%;
    padding: 10px;
    box-shadow: 0 0 5px #ffdfdf;
    border-radius: 5px;
    overflow: hidden;
}
.card .top {
    text-align: center;
}
.card p {
    font-weight: bold;
    color: #fe0000;
}
.card button {
    outline: 0;
    border: 0;
	color: #fff;
	border-radius: 4px;
	cursor: pointer;
	font-weight: 400;
	padding: 8px 13px;
  width: 100%;
  background: #fe0000;
}

.card .drag-area {
	height: 150px;
	border-radius: 5px;
	border: 2px dashed #fe0000;
	color: #fe0000;
	background: #f4f3f9;
	display: flex;
	justify-content: center;
	align-items: center;
	user-select: none;
	-webkit-user-select: none;
	margin-top: 10px;
}
.card .drag-area .visible {
	font-size: 18px;
}
.card .select{
    color: #5256ad;
	margin-left: 5px;
	cursor: pointer;
	transition: 0.4s;
}
.card .select:hover {
	opacity: 0.6;
}
.card .container {
	width: 100%;
	height: auto;
	display: flex;
	justify-content: flex-start;
	align-items: flex-start;
	flex-wrap: wrap;
	max-height: 200px;
	overflow-y: auto;
	margin-top: 10px;
}
.card .container .image {
	width: 75px;
	margin-right: 5px;
	height: 75px;
	position: relative;
	margin-bottom: 8px;
}
.card .container .image img {
	width: 100%;
	height: 100%;
	border-radius: 5px;
}
.card .container .image span {
	position: absolute;
	top: -2px;
	right: 9px;
	font-size: 20px;
	cursor: pointer;
}
.card input,
.card .drag-area .on-drop, 
.card .drag-area.dragover .visible {
	display: none;
}
.delete {
  z-index: 999;
  color: #fe0000;
}
</style>
