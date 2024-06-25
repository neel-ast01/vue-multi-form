<template>
  <div>
    <h2>Summary</h2>
    <ul>
      <li><strong>First Name:</strong> {{ formData.firstName }}</li>
      <li><strong>Last Name:</strong> {{ formData.lastName }}</li>
      <li><strong>Email:</strong> {{ formData.email }}</li>
      <li><strong>Phone:</strong> {{ formData.phone }}</li>
      <li><strong>Address:</strong> {{ formData.address }}</li>
      <li><strong>Highest Degree:</strong> {{ formData.highestDegree }}</li>
      <li><strong>Institution:</strong> {{ formData.institution }}</li>
      <li><strong>Graduation Year:</strong> {{ formData.graduationYear }}</li>
      <li><strong>Major:</strong> {{ formData.major }}</li>
      <li><strong>GPA:</strong> {{ formData.gpa }}</li>
      <li><strong>Company Name:</strong> {{ formData.companyName }}</li>
      <li><strong>Role:</strong> {{ formData.role }}</li>
      <li><strong>Duration:</strong> {{ formData.duration }}</li>
      <li><strong>Responsibilities:</strong> {{ formData.responsibilities }}</li>
      <li>
        <strong>File:</strong>
        {{ formData.file ? formData.file.name : "No file uploaded" }}
      </li>
      <li v-if="formData.file">
        <strong>Image:</strong>
        <img :src="formDataFileUrl" alt="Uploaded Image" width="100" height="100" />
      </li>
    </ul>
    <button @click="$emit('prev-step')">Previous</button>
    <!-- <button @click="$emit('submit-form')">Submit</button> -->
    <button @click="resetForm">Reset All Values</button>
  </div>
</template>

<script>
export default {
  props: ["formData"],
  computed: {
    formDataFileUrl() {
      return this.formData.file ? URL.createObjectURL(this.formData.file) : "";
    },
  },
  methods: {
    resetForm() {
      this.$emit("reset-form");
    },
  },
};
</script>

<style scoped>
/* Add your styles here */
</style>
