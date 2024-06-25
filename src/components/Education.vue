<template>
  <div>
    <h2>Education</h2>
    <div>
      <label for="highestDegree">Highest Degree</label>
      <input
        type="text"
        id="highestDegree"
        v-model="formData.highestDegree"
        @blur="validateField('highestDegree')"
      />
      <span v-if="errors.highestDegree" class="error">{{ errors.highestDegree }}</span>
    </div>

    <div>
      <label for="institution">Institution</label>
      <input
        type="text"
        id="institution"
        v-model="formData.institution"
        @blur="validateField('institution')"
      />
      <span v-if="errors.institution" class="error">{{ errors.institution }}</span>
    </div>

    <div>
      <label for="graduationYear">Graduation Year</label>
      <input
        type="text"
        id="graduationYear"
        v-model="formData.graduationYear"
        @blur="validateField('graduationYear')"
      />
      <span v-if="errors.graduationYear" class="error">{{ errors.graduationYear }}</span>
    </div>

    <div>
      <label for="major">Major</label>
      <input
        type="text"
        id="major"
        v-model="formData.major"
        @blur="validateField('major')"
      />
      <span v-if="errors.major" class="error">{{ errors.major }}</span>
    </div>

    <div>
      <label for="gpa">GPA</label>
      <input type="text" id="gpa" v-model="formData.gpa" @blur="validateField('gpa')" />
      <span v-if="errors.gpa" class="error">{{ errors.gpa }}</span>
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
        highestDegree: "",
        institution: "",
        graduationYear: "",
        major: "",
        gpa: "",
      },
    };
  },
  methods: {
    validateField(field) {
      switch (field) {
        case "highestDegree":
          this.errors.highestDegree = this.formData.highestDegree
            ? ""
            : "Highest Degree is required";
          break;
        case "institution":
          this.errors.institution = this.formData.institution
            ? ""
            : "Institution is required";
          break;
        case "graduationYear":
          this.errors.graduationYear = this.formData.graduationYear
            ? ""
            : "Graduation Year is required";
          break;
        case "major":
          this.errors.major = this.formData.major ? "" : "Major is required";
          break;
        case "gpa":
          this.errors.gpa = this.formData.gpa ? "" : "GPA is required";
          break;
      }
    },
    validateForm() {
      this.validateField("highestDegree");
      this.validateField("institution");
      this.validateField("graduationYear");
      this.validateField("major");
      this.validateField("gpa");

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
