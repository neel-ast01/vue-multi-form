<template>
  <div>
    <h2>Work Experiences</h2>
    <div>
      <label for="companyName">Company Name</label>
      <input
        type="text"
        id="companyName"
        v-model="formData.companyName"
        @blur="validateField('companyName')"
      />
      <span v-if="errors.companyName" class="error">{{ errors.companyName }}</span>
    </div>

    <div>
      <label for="role">Role</label>
      <input
        type="text"
        id="role"
        v-model="formData.role"
        @blur="validateField('role')"
      />
      <span v-if="errors.role" class="error">{{ errors.role }}</span>
    </div>

    <div>
      <label for="duration">Duration</label>
      <input
        type="text"
        id="duration"
        v-model="formData.duration"
        @blur="validateField('duration')"
      />
      <span v-if="errors.duration" class="error">{{ errors.duration }}</span>
    </div>

    <div>
      <label for="responsibilities">Responsibilities</label>
      <input
        type="text"
        id="responsibilities"
        v-model="formData.responsibilities"
        @blur="validateField('responsibilities')"
      />
      <span v-if="errors.responsibilities" class="error">{{
        errors.responsibilities
      }}</span>
    </div>

    <div>
      <button @click="$emit('prev-step')">Previous</button>
      <button @click="validateAndNextStep">Next</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["formData"],
  data() {
    return {
      errors: {
        companyName: "",
        role: "",
        duration: "",
        responsibilities: "",
      },
    };
  },
  methods: {
    validateField(field) {
      switch (field) {
        case "companyName":
          this.errors.companyName = this.formData.companyName
            ? ""
            : "Company Name is required";
          break;
        case "role":
          this.errors.role = this.formData.role ? "" : "Role is required";
          break;
        case "duration":
          this.errors.duration = this.formData.duration ? "" : "Duration is required";
          break;
        case "responsibilities":
          this.errors.responsibilities = this.formData.responsibilities
            ? ""
            : "Responsibilities is required";
          break;
      }
    },
    validateForm() {
      this.validateField("companyName");
      this.validateField("role");
      this.validateField("duration");
      this.validateField("responsibilities");

      return !Object.values(this.errors).some((error) => error);
    },
    validateAndNextStep() {
      if (this.validateForm()) {
        this.$emit("next-step");
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
