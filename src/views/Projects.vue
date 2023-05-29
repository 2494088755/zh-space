<template>
  <div class="projects">
    <h1>图片展示墙</h1>
    <el-upload
        action="http://8.130.70.247:8081/api/upload"
        :on-success="handleUploadSuccess"
        :show-file-list="false"
        accept="image/*"
    >
      <el-button type="primary">上传图片</el-button>
    </el-upload>
    <div class="gallery">
      <el-image
          v-for="(image, index) in images"
          :key="index"
          :src="image.thumbnail"
          :preview-src-list="image.previewSrcList"
          :fit="'contain'"
          class="thumbnail"
          @click="viewImage(index)"
      ></el-image>
    </div>
    <el-dialog :visible.sync="dialogVisible" width="60%">
      <el-image :src="currentImage"></el-image>
      <span slot="footer" class="dialog-footer">
    <el-button type="primary" @click="dialogVisible = false">关闭</el-button>
    <el-button @click="downloadImage">下载图片</el-button>
  </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      images: [],
      dialogVisible: false,
      currentImage: '',
    };
  },
  methods: {
    async fetchImages() {
      try {
        const response = await fetch('http://8.130.70.247:8081/api/images');
        const imageFilenames = await response.json();
        this.images = imageFilenames.map(filename => ({
          thumbnail: `http://8.130.70.247:8081/api/files/${filename}`,
          previewSrcList: [`http://8.130.70.247:8081/api/files/${filename}`],
        }));
      } catch (error) {
        console.error('Error fetching images:', error);
      }
    },
    handleUploadSuccess(response, file) {
      this.images.push({
        thumbnail: URL.createObjectURL(file.raw),
        previewSrcList: [URL.createObjectURL(file.raw)],
      });
    },
    viewImage(index) {
      this.currentImage = this.images[index].previewSrcList[0];
      this.dialogVisible = true;
    },
    downloadImage() {
      const link = document.createElement('a');
      link.href = this.currentImage;
      link.download = 'image.jpg';
      link.click();
    },
  },
  mounted() {
    this.fetchImages();
  },
};
</script>

<style scoped>
.projects {
  text-align: center;
  padding: 1rem;
}

.gallery {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.thumbnail {
  width: 150px;
  height: 150px;
  margin: 10px;
  cursor: pointer;
  border: 1px solid #eee;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
</style>
