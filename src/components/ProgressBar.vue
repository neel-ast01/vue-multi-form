<template>
  <div class="progress-bar-container">
    <ul class="progressbar">
      <li
        v-for="(step, index) in steps"
        :key="index"
        :class="{
          active: index + 1 <= currentStep,
          clickable: index + 1 <= currentStep,
          hoverable: index + 1 === currentStep,
        }"
        @click="handleClick(index + 1)"
        @mouseover="handleHover(index + 1)"
      >
        <div class="icon">{{ step.icon }}</div>
        <div class="title">{{ step.title }}</div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    currentStep: {
      type: Number,
      required: true,
    },
    totalSteps: {
      type: Number,
      required: true,
    },
    steps: {
      type: Array,
      required: true,
    },
  },
  emits: ["step-click", "step-hover"],
  methods: {
    handleClick(index) {
      if (this.canClick(index)) {
        this.$emit("step-click", index);
      }
    },
    handleHover(index) {
      if (index <= this.currentStep) {
        this.$emit("step-hover", index);
      }
    },
    canClick(index) {
      return index < this.currentStep;
    },
  },
};
</script>

<style scoped>
.progress-bar-container {
  width: 125%;
  margin: 20px 0;
}

.progressbar {
  display: flex;
  justify-content: space-around;
  list-style: none;
  padding: 0;
  counter-reset: step;
}

.progressbar li {
  position: relative;
  flex: 1;
  text-align: center;
  cursor: not-allowed;
}

.progressbar li:before {
  content: counter(step);
  counter-increment: step;
  width: 30px;
  height: 30px;
  line-height: 30px;
  border: 2px solid #bebebe;
  background: white;
  border-radius: 50%;
  display: inline-block;
  color: #bebebe;
}

.progressbar li:after {
  content: "";
  position: absolute;
  width: 100%;
  height: 2px;
  background: #bebebe;
  top: 15px;
  left: -50%;
  z-index: -1;
}

.progressbar li:first-child:after {
  content: none;
}

.progressbar li.active:before,
.progressbar li.active:hover:before {
  border-color: #3aac5d;
  background: #3aac5d;
  color: white;
  cursor: pointer;
}

.progressbar li.active:after {
  background: #3aac5d;
}

.progressbar li.clickable {
  cursor: pointer;
}

.progressbar li.hoverable:hover:before {
  border-color: #3aac5d;
  background: #3aac5d;
  color: white;
}

.progressbar li .icon {
  font-size: 20px;
}

.progressbar li .title {
  margin-top: 5px;
  font-size: 14px;
}
</style>
