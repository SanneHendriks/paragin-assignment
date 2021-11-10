user selector designed to select one user for a task, selecting yourself has a dedicated interaction flow
example:
<!--
  <UserSelector v-model="selectedUserID" :users="usersArray" userText="user" taskText="task"/>
-->

<template>
  <div class="radio-btn-group">
    <button id="userselector-btn-other" :class="{ selected: !meSelected }" @click.prevent="meSelected = false">
      <label for="userselector-btn-other">One {{ userText }}</label>
    </button>
    <button id="userselector-btn-me" :class="{ selected: meSelected }" @click.prevent="meSelected = true">
      <label for="userselector-btn-me">Assigned to me</label>
    </button>
  </div>

  <div class="alert capitalize" v-if="selectedUser">
    {{ taskText }} is assigned to: <b>{{ meSelected ? 'Assigned to me' : selectedUserComposedName }}.</b> You don’t need to specify anything else.
  </div>
  <div class="alert warning" v-else>
    Please select a {{ userText }} from the list below in order to assign your {{ taskText }}.
  </div>

  <div v-if="!meSelected" class="user-table-outer-container">
    <div class="user-table-inner-container">
      <h4>All {{ userText }}s</h4>
      <table>
        <tr>
          <th>Name</th>
          <th>Role</th>
          <th>Group</th>
          <th></th>
        </tr>
        <tr v-for="user in usersFilteredSorted" :key="user.id">
          <td class="capitalize">{{ user.lastName }}, {{ user.initials }}</td>
          <td>{{ user.role }}</td>
          <td>{{ user.group }}</td>
          <td v-if="modelValue != user.id"><button class="btn small green" @click.prevent="$emit('update:modelValue', user.id)">Select this {{ userText }}</button></td>
          <td v-else><button class="btn small red" @click.prevent="$emit('update:modelValue', null)">Remove</button></td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UserSelector',
  props: {
    modelValue: {
      required: true,
    },
    users: Array,
    userText: {
      type: String,
      default: "user",
    },
    taskText: {
      type: String,
      default: "task",
    },
  },
  emits: ['update:modelValue'],
  computed: {
    // returns selected user object, null if none is selected or found
    selectedUser() {
      if (this.modelValue) {
        return this.users.find(user => user.id == this.modelValue);
      }
      return null;
    },
    // returns selected user composed name, null if none is selected or found
    selectedUserComposedName() {
      if (this.selectedUser) {
        return this.selectedUser.lastName + ", " + this.selectedUser.initials;
      }
      return null;
    },
    // transforms the selected user id (modelValue) to whether the current user is selected
    // setting it to true assigns current user id
    // setting it to false unassigns the current user if assigned
    meSelected: {
      get() {
        if (this.selectedUser) {
          return this.selectedUser.me;
        }
        return false;
      },
      set(newValue) {
        let me = this.users.find(user => user.me);
        if (me) {
          if (newValue) {
            this.$emit('update:modelValue', me.id);
          } else if (this.modelValue == me.id) {
            this.$emit('update:modelValue', null);
          }
        }
      }
    },
    // returns the users filtered and sorted
    usersFilteredSorted() {
      return this.users.filter(user => {
        return !user.me && (!this.selectedUser || this.selectedUser === user);
      });
    }
  },
}
</script>

<style scoped>
.capitalize:first-letter {
  text-transform: capitalize;
}
.radio-btn-group {
  display: flex;
  padding: 8px;
  background: #F1F1F1;
  margin-bottom: 10px;
}
.radio-btn-group button {
  flex-grow: 1;
  font-size: 12px;
  background: none;
  border: 0;
  color: #111111;
  width: 20px;
}
.radio-btn-group .selected {
  background: #3273F6;
  border-radius: 60px;
  padding: 8px;
  font-weight: 700;
  color: #FFFFFF;
}
.alert {
  padding: 10px;
  background: rgba(50, 115, 246, 0.1);
  border: 1px solid #3273F6;
  margin-bottom: 10px;
}
.alert.warning {
  background: #FEF9E6;
  border: 1px solid #F9D860;
}
.user-table-outer-container {
  padding: 10px;
  background: rgba(91, 160, 18, 0.1);
}
.user-table-inner-container {
  background: #FFFFFF;
  border: 1px solid #A4A4A4;
  border-radius: 3px;
  max-height: 460px;
  overflow-y: auto;
}
h4 {
  font-weight: 400;
  font-size: 14px;
  padding: 14px 0 10px 0;
  margin: 0 20px;
  border-bottom: 1px solid #A4A4A4;
}
table {
  width: 100%;
}
tr:nth-child(even) {
  background: #F1F1F1;
}
th, td {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-right: 20px;
  text-align: left;
}
th {
  padding-top: 18px;
}
th:first-child, td:first-child {
  padding-left: 20px;
  padding-right: 0;
}
th:last-child, td:last-child {
  text-align: right;
}
table, th, td {
  border: 0;
  border-collapse: collapse;
}
</style>