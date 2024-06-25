<template>
  <div>
    <!-- <ProgressBar
        :currentStep="currentStep"
        :totalSteps="totalSteps"
        @step-click="handleStepClick"
        @step-hover="handleStepHover"
      /> -->
    <ProgressBar
      :currentStep="currentStep"
      :totalSteps="5"
      :steps="steps"
      @step-click="handleStepClick"
      @step-hover="handleStepHover"
    />
    <Profile v-if="currentStep === 1" :formData="formData" @next-step="nextStep" />

    <div v-if="currentStep === 1">
      <PersonalInfo :formData="formData" @next-step="nextStep" />
    </div>
    <div v-if="currentStep === 2">
      <Education :formData="formData" @next-step="nextStep" @prev-step="prevStep" />
    </div>
    <div v-if="currentStep === 3">
      <WorkExperiences :formData="formData" @next-step="nextStep" @prev-step="prevStep" />
    </div>
    <div v-if="currentStep === 4">
      <UserPhoto :formData="formData" @next-step="nextStep" @prev-step="prevStep" />
    </div>
    <div v-if="currentStep === 5">
      <Summary :formData="formData" @prev-step="prevStep" @reset-form="resetFormData" />
    </div>
  </div>
</template>

<script>
import PersonalInfo from "./PersonalInfo.vue";
import Education from "./Education.vue";
import WorkExperiences from "./WorkExperiences.vue";
import UserPhoto from "./UserPhoto.vue";
import ProgressBar from "./ProgressBar.vue";
import Summary from "./Summary.vue";


export default {
  components: {
    PersonalInfo,
    Education,
    WorkExperiences,
    UserPhoto,
    ProgressBar,
    Summary,
  },
  data() {
    return {
      currentStep: 1,
      totalSteps: 5,
      formData: {
        firstName: "",
        lastName: "",
        email: "",
        phone: "",
        address: "",
        highestDegree: "",
        institution: "",
        graduationYear: "",
        major: "",
        gpa: "",
        companyName: "",
        role: "",
        duration: "",
        responsibilities: "",
        file: null,
      },
      steps: [
        { icon: "👤", title: "Profile" },
        { icon: "🎓", title: "Education" },
        { icon: "💼", title: "Work" },
        { icon: "📸", title: "Photo" },
        { icon: "🤷‍♀️", title: "Summary" },
      ],
    };
  },
  methods: {
    handleStepClick(step) {
      this.currentStep = step;
    },
    handleStepHover(step) {
      console.log("Hovered over step", step);
    },
    nextStep() {
      this.currentStep++;
    },
    prevStep() {
      this.currentStep--;
    },
    submitForm() {
      // Handle form submission, e.g., send data to a server
      console.log(this.formData);
      alert("Form submitted successfully!");
    },
    resetFormData() {
      this.formData = {
        firstName: "",
        lastName: "",
        email: "",
        phone: "",
        address: "",
        highestDegree: "",
        institution: "",
        graduationYear: "",
        major: "",
        gpa: "",
        companyName: "",
        role: "",
        duration: "",
        responsibilities: "",
        file: null,
      };
      this.currentStep = 1;
    },
  },
};
</script>

<style scoped>
/* Add your styles here */
</style>
