<template>
  <div class="container-fluid bg-dark text-white custom-row ">
    <div class="table-responsive">
      <table class="table table-dark table-bordered table-hover ">
        <thead>
          <tr class="bg-primary ">
            <th ></th>
            <th>End of Contracts</th>
            <th>Option</th>
            <th>Option - Validity</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="player in allPlayers" :key="player.id" >
            <td class="custom-row ">
              <PlayerComponent :user="player"/>
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
import { ref } from 'vue';
import PlayerComponent from './player/playerComponent.vue';
import { players } from "@/data/data.js";

const allPlayers = ref(players);

const formatDate = (dateString) => {
  if (!dateString) return '--';
  const date = new Date(dateString);
  const day = String(date.getDate()).padStart(2, '0');
  const month = String(date.getMonth() + 1).padStart(2, '0'); // Les mois commencent à 0
  const year = date.getFullYear();
  return `${day} - ${month} - ${year}` ;
};

</script>

<style scoped>


.vertical-center {
  vertical-align: middle;
}


.custom-row td  {
  border: none;
}

.custom-row th  {
  border: none;
}

</style>