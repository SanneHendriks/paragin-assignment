<template>
  <button class="btn-openmodal" @click="this.modalOpen = true">show correction round manager</button>
  <Modal v-model="modalOpen">
    <template v-slot:title>Add new correction round</template>
    <template v-slot:default>
      <CorrectionRoundManager v-bind="settings" @update="settings = $event" :users="fakeUsers"/>
    </template>
  </Modal>
  <br>
  <div>saved state: {{ settings }}</div>
</template>

<script>
import CorrectionRoundManager from './components/CorrectionRoundManager.vue'
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    CorrectionRoundManager,
    Modal,
  },
  data() {
    return {
      modalOpen : true,
      settings: {},
      fakeUsers: [
        {
          initials: "S",
          lastName: "Hendriks",
          role: "Developer",
          group: "Applicants",
          id: 1,
          me: true,
        },{
          initials: "C",
          lastName: "van den Endelagen",
          role: "Test Coordinator",
          group: "Paragin Medewerkers Group XAAS",
          id: 2,
        }, {
          initials: "A",
          lastName: "Smit",
          role: "Test Coordinator",
          group: "Paragin Medewerkers Group XAAS",
          id: 3,
        }, {
          initials: "C",
          lastName: "de Jong",
          role: "Test Coordinator",
          group: "Paragin Medewerkers Group XAAS",
          id: 4,
        }, {
          initials: "G",
          lastName: "Janssen",
          role: "Test Coordinator",
          group: "Paragin Medewerkers Group XAAS",
          id: 5,
        }, {
          initials: "C",
          lastName: "Peters",
          role: "Test Coordinator",
          group: "Paragin Medewerkers Group XAAS",
          id: 6,
        }, {
          initials: "F",
          lastName: "Dijkstra",
          role: "Test Coordinator",
          group: "Paragin Medewerkers Group XAAS",
          id: 7,
        }, {
          initials: "T",
          lastName: "van der Linden",
          role: "Test Coordinator",
          group: "Paragin Medewerkers Group XAAS",
          id: 8,
        }, {
          initials: "C",
          lastName: "Willems",
          role: "Test Coordinator",
          group: "Paragin Medewerkers Group XAAS",
          id: 9,
        }, {
          initials: "C",
          lastName: "Hoekstra",
          role: "Test Coordinator",
          group: "Paragin Medewerkers Group XAAS",
          id: 10,
        }, {
          initials: "C",
          lastName: "Peeters",
          role: "Test Coordinator",
          group: "Paragin Medewerkers Group XAAS",
          id: 11,
        },
      ]
    }
  },
}
</script>

<style>
body {
  margin: 0;
}
#app {
  font-family: Arial;
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  color: #111111;
  margin: 20px;
}
.btn-openmodal {
  margin-bottom: 20px;
}
.btn {
  font-weight: 700;
  font-size: 12px;
  color: #111111;
  border: 1px solid #111111;
  border-radius: 3px;
  background: none;
  padding: 7px 10px;
  white-space: nowrap;
}
.btn.solid {
  background: #111111;
}
.btn.green {
  border: 1px solid #5BA012;
  color: #5BA012;
}
.btn.green.solid {
  background: #5BA012;
}
.btn.red {
  border: 1px solid #CF191E;
  color: #CF191E;
}
.btn.red.solid {
  background: #CF191E;
}
.btn.solid {
  color: #FFFFFF;
}
.btn.small {
  font-size: 10px;
}
</style>
