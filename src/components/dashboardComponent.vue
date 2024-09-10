<template>
  <div class="container-fluid bg-dark text-white custom-row ">
    <div class="table-responsive">
      <table class="table table-dark table-bordered table-hover">
        <thead>
          <tr class="bg-primary">
            <th></th>
            <th>
              End of Contracts
              <button @click="toggleSortDirection" class="btn btn-sm btn-light ms-2">
                {{ sortDirection === 'asc' ? '▲' : '▼' }}
              </button>
            </th>
            <th>Option</th>
            <th>Option - Validity</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="player in sortedPlayers" :key="player.id">
            <td class="custom-row">
              <PlayerComponent :user="player" />
            </td>
            <td class="vertical-center" :style="{ color: player.contract_end_status }">
              {{ formatDate(player.contract_end) }}
            </td>
            <td class="vertical-center">
              {{ player.option ? player.option : '--' }}
            </td>
            <td class="vertical-center">
              {{ player.option_validity ? formatDate(player.option_validity) : '--' }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>

import { ref, computed } from 'vue';
import PlayerComponent from './player/playerComponent.vue';
import { players } from "@/data/data.js";


// Référence à la liste des joueurs
const allPlayers = ref(players);


// Formater les dates
const formatDate = (dateString) => {
  if (!dateString) return '--';
  const date = new Date(dateString);
  const day = String(date.getDate()).padStart(2, '0');
  const month = String(date.getMonth() + 1).padStart(2, '0'); 
  const year = date.getFullYear();
  return `${day} - ${month} - ${year}`;
};


// Direction du tri
const sortDirection = ref('asc');


// Fonction pour basculer le tri
const toggleSortDirection = () => {
  sortDirection.value = sortDirection.value === 'asc' ? 'desc' : 'asc';
};


// Trie en fonction des dates
const sortedPlayers = computed(() => {
  return [...allPlayers.value].sort((a, b) => {
    const dateA = new Date(a.contract_end);
    const dateB = new Date(b.contract_end);
    return sortDirection.value === 'asc' ? dateA - dateB : dateB - dateA;
  });
});


</script>


<style scoped>
.vertical-center {
  vertical-align: middle;
}

.custom-row td, th {
  border: none;
}
</style>
