<script setup>
import { ref } from 'vue';
import HomeScreen from './components/HomeScreen.vue';
import ExpenseScreen from './components/ExpenseScreen.vue';
import SummaryScreen from './components/SummaryScreen.vue';
 
const currentScreen = ref('home');
const group = ref([]);
const expenseData = ref({
  total: 0,
  payers: []
});
 
function handleGroup(newGroup) {
  group.value = newGroup;
  currentScreen.value = 'expense';
}
 
function goToSummary(data) {
  expenseData.value = data;
  currentScreen.value = 'summary';
}
 
function resetApp() {
  group.value = [];
  expenseData.value = { total: 0, payers: [] };
  currentScreen.value = 'home';
}
</script>
 
<template>
  <div class="p-6">
    <HomeScreen v-if="currentScreen === 'home'" @groupCreated="handleGroup" />
    <ExpenseScreen
      v-if="currentScreen === 'expense'"
      :array="group"
      @goToSummary="goToSummary"
    />
    <SummaryScreen
      v-if="currentScreen === 'summary'"
      :group="group"
      :total="expenseData.total"
      :payers="expenseData.payers"
      @reset="resetApp"
    />
  </div>
</template>