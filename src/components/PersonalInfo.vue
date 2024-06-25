<template>
  <div>
    <h2>Profile</h2>
    <div>
      <label for="firstName">First Name</label>
      <input
        type="text"
        id="firstName"
        v-model="formData.firstName"
        @blur="validateField('firstName')"
      />
      <span v-if="errors.firstName" class="error">{{ errors.firstName }}</span>
    </div>

    <div>
      <label for="lastName">Last Name</label>
      <input
        type="text"
        id="lastName"
        v-model="formData.lastName"
        @blur="validateField('lastName')"
      />
      <span v-if="errors.lastName" class="error">{{ errors.lastName }}</span>
    </div>

    <div>
      <label for="email">Email</label>
      <input
        type="email"
        id="email"
        v-model="formData.email"
        @blur="validateField('email')"
      />
      <span v-if="errors.email" class="error">{{ errors.email }}</span>
    </div>

    <div>
      <label for="phone">Phone</label>
      <input
        type="tel"
        id="phone"
        v-model="formData.phone"
        @blur="validateField('phone')"
      />
      <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
    </div>

    <div>
      <label for="address">Address</label>
      <input
        type="text"
        id="address"
        v-model="formData.address"
        @blur="validateField('address')"
      />
      <span v-if="errors.address" class="error">{{ errors.address }}</span>
    </div>

    <button @click="validateAndNextStep">Next</button>
  </div>
</template>

<script>
export default {
  props: ["formData"],
  data() {
    return {
      errors: {
        firstName: "",
        lastName: "",
        email: "",
        phone: "",
        address: "",
      },
      emailRegex: /^[^\s@]+@[^\s@]+\.[^\s@]+$/,
      phoneRegex: /^\d{10}$/,
    };
  },
  methods: {
    validateField(field) {
      switch (field) {
        case "firstName":
          this.errors.firstName = this.formData.firstName ? "" : "First Name is required";
          break;
        case "lastName":
          this.errors.lastName = this.formData.lastName ? "" : "Last Name is required";
          break;
        case "email":
          if (!this.formData.email) {
            this.errors.email = "Email is required";
          } else if (!this.emailRegex.test(this.formData.email)) {
            this.errors.email = "Email is invalid";
          } else {
            this.errors.email = "";
          }
          break;
        case "phone":
          if (!this.formData.phone) {
            this.errors.phone = "Phone is required";
          } else if (!this.phoneRegex.test(this.formData.phone)) {
            this.errors.phone = "Phone must be exactly 10 digits";
          } else {
            this.errors.phone = "";
          }
          break;
        case "address":
          this.errors.address = this.formData.address ? "" : "Address is required";
          break;
      }
    },
    validateForm() {
      this.validateField("firstName");
      this.validateField("lastName");
      this.validateField("email");
      this.validateField("phone");
      this.validateField("address");

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
