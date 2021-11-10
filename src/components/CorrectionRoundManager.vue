settings relating to a correction round
example:
<!--
  <CorrectionRoundManager v-bind="settingsObject" @update="settingsObject = $event" :users="usersArray"/>
-->

<template>
  <form class="outer-container" @submit.prevent="onSubmit">

    <div class="inner-container">
      <h3>Correction round settings</h3>
      <div class="zebrabox">
        <InputNY v-model="localAnonymous">
          Anonymous correction round
        </InputNY>
        <InputNY v-model="localShowPreviousScores">
          Show scores and feedback from previous correction rounds
        </InputNY>
        <InputNY v-model="localPreviousRoundsMustBeCompleted">
          Previous correction rounds must be completed before this one can start
        </InputNY>
        <InputNY v-model="localEditableAfterChecking">
          After checking, the score and feedback can be edited
        </InputNY>
        <InputNY v-model="localWillUpdateResults">
          The result and grade will be updated based on this correction round
        </InputNY>
        <InputSlider v-model="localDeadline">
          Deadline, the number of days within which the result has to be checked after submission
        </InputSlider>
      </div>
    </div>

    <div class="inner-container">
      <h3>Correction distribution</h3>
      <p>Corrections should be assigned to:</p>
      <UserSelector v-model="localCorrectorId" :users="users"
        userText="corrector" taskText="correction distribution"/>
    </div>

    <div class="footer">
      <button class="btn green">Cancel</button>
      <input class="btn solid" :class="dataValid ? 'green' : 'red'" :disabled="!dataValid" type="submit" value="Save this correction round">
    </div>

  </form>
</template>

<script>
import InputNY from './InputNY.vue'
import InputSlider from './InputSlider.vue'
import UserSelector from './UserSelector.vue'

export default {
  name: 'CorrectionRoundManager',
  components: {
    InputNY,
    InputSlider,
    UserSelector,
  },
  props: {
    anonymous: {
      type: Boolean,
      default: false
    },
    showPreviousScores: {
      type: Boolean,
      default: false
    },
    previousRoundsMustBeCompleted: {
      type: Boolean,
      default: false
    },
    editableAfterChecking: {
      type: Boolean,
      default: false
    },
    willUpdateResults: {
      type: Boolean,
      default: true
    },
    deadline: {
      type: Number,
      default: 14
    },
    correctorId: {
      type: [String, Number],
    },
    users: Array,
  },
  data() {
    return {
      localAnonymous: this.anonymous,
      localShowPreviousScores: this.showPreviousScores,
      localPreviousRoundsMustBeCompleted: this.previousRoundsMustBeCompleted,
      localEditableAfterChecking: this.editableAfterChecking,
      localWillUpdateResults: this.willUpdateResults,
      localDeadline: this.deadline,
      localCorrectorId: this.correctorId,
    }
  },
  computed: {
    // checks if the form data is ready for submission
    dataValid() {
      return typeof this.localCorrectorId === 'number' || typeof this.localCorrectorId === 'string';
    },
  },
  methods: {
    onSubmit() {
      this.$emit('update', {
        anonymous: this.localAnonymous,
        showPreviousScores: this.localShowPreviousScores,
        previousRoundsMustBeCompleted: this.localPreviousRoundsMustBeCompleted,
        editableAfterChecking: this.localEditableAfterChecking,
        willUpdateResults: this.localWillUpdateResults,
        deadline: this.localDeadline,
        correctorId: this.localCorrectorId,
      });
    },
  },
}
</script>

<style scoped>
.outer-container {
  padding-top: 8px;
}
.inner-container {
  padding: 20px;
  background: #FAFAFA;
  border: 1px solid #ECECEC;
  margin: 0 8px 10px 8px;
}
.footer {
  padding: 10px;
  background: #FAFAFA;
  box-shadow: 0px -4px 10px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
h3 {
  font-size: 16px;
  font-weight: 400;
  color: #4A4A4A;
  margin: 0 0 20px 0;
}
p {
  margin: 0;
  margin-bottom: 10px;
}
.zebrabox div:nth-child(odd) {
  background: #F1F1F1;
}
</style>