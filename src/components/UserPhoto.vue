<template>
  <div>
    <h2>Upload Photo</h2>
    <div>
      <label for="file">Upload File</label>
      <input type="file" id="file" @change="handleFileUpload" />
      <span v-if="errors.file" class="error">{{ errors.file }}</span>
    </div>

    <div>
      <button @click="$emit('prev-step')">Previous</button>
      <button @click="validateAndSubmit">Submit</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["formData"],
  data() {
    return {
      errors: {
        file: "",
      },
    };
  },
  methods: {
    handleFileUpload(event) {
      this.formData.file = event.target.files[0];
      this.validateField("file");
    },
    validateField(field) {
      if (field === "file") {
        this.errors.file = this.formData.file ? "" : "File is required";
      }
    },
    validateForm() {
      this.validateField("file");

      return !this.errors.file;
    },
    validateAndSubmit() {
      if (this.validateForm()) {
        this.$emit("next-step");
        this.$emit("submit-form");
      }
    },
  },
};
</script>

<style scoped>
.error {
  color: red;
  font-size: 12px;
  margin-top: 5px;
  display: block;
}
</style>
