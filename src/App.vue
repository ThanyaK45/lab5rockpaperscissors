<script setup>

import { ref } from 'vue';

// กำหนดตัวแปร
const ai_random = ref('');
const player = ref('');
const result = ref('');
const ai_point = ref(0) //เอาไว้เก็บคะแนน player
const player_point = ref(0) //เอาไว้เก็บคะแนน ai
const tie_point = ref(0) // คะแนนเสมอ
const isResetting = ref(false);

const choices = ['rock', 'paper', 'scissors', 'love'];

// function ของผู้เล่น 
const selectOption = (choice) => {
  player.value = choice;
};

// เริ่มเกมเมื่อผู้เล่นกดปุ่มตกลง
function startGame() {
  if (player.value) {
    playGame();
  }
}

// function เกมเป่ายิ๊งฉุบ
const playGame = () => {
  const computer = choices[Math.floor(Math.random() * 4)];
  ai_random.value = computer;

  if (player.value === computer) {
    result.value = 'Draw';
    tie_point.value += 1;
  } else if (
    (player.value === 'rock' && computer === 'scissors') ||
    (player.value === 'paper' && computer === 'rock') ||
    (player.value === 'scissors' && computer === 'paper')||
    (player.value === 'love' && computer === 'paper')||
    (player.value === 'love' && computer === 'rock')||
    (player.value === 'love' && computer === 'scissors')
  ) {
    result.value = 'Player Win!!!';
    player_point.value += 1;
  } else {
    result.value = 'AI Win!!!';
    ai_point.value += 1;
  }
};

// function เริ่มเกมใหม่
function resetGame() {
  isResetting.value = true; // เปิดการรีเซ็ต
}

function reset() {
  player_point.value = 0;
  ai_point.value = 0;
  tie_point.value = 0;
  isResetting.value = false; // ปิดการรีเซ็ต
}


</script>

<template>

  <div>
    <h1>Rock Paper Scissors (and Love?) Game</h1>

    <!-- เลือกตัวเลือก -->
    <div>
      <button @click="selectOption('rock')" style=";">Rock</button>
      <button @click="selectOption('paper')" style=";">Paper</button>
      <button @click="selectOption('scissors')" style=";">Scissors</button>
      <button @click="selectOption('love')" style=";">Love</button>
    </div>

    <div class="picture-ai-player">

      <!-- แสดงผล -->
      <div class="ai-pic">
        <h1>AI</h1>
        <p v-if="ai_random == ''"><img style="height: 200px; margin-left: 0px;" src="./assets/ai.png" alt="" ></p>
        <p v-else-if="ai_random == 'rock'"><img style="margin-top: 28px; height: 150px;" src="./assets/rock.png" alt=""></p>
        <p v-else-if="ai_random == 'paper'"><img style="margin-top: 50px; height: 110px;" src="./assets/paper.png" alt=""></p>
        <p v-else-if="ai_random == 'scissors'"><img style="margin-top: 10px; height: 190px;" src="./assets/scissors.png" alt=""></p>
        <p v-else-if="ai_random == 'love'"><img style="margin-top: 10px; height: 180px;" src="./assets/love.png" alt=""></p>
      </div>

      <div class="player-pic">
        <h1 style="margin-left: 150px;">Player</h1>
        <p v-if="player == ''"><img style="height: 200px; margin-left: 150px;" src="./assets/player.png" alt="" ></p>
        <p v-else-if="player == 'rock'"><img style="margin-top: 28px; margin-left: 150px; height: 150px;" src="./assets/rock.png" alt=""></p>
        <p v-else-if="player == 'paper'"><img style="margin-top: 50px; margin-left: 150px; height: 110px;" src="./assets/paper.png" alt=""></p>
        <p v-else-if="player == 'scissors'"><img style="margin-top: 10px; margin-left: 150px; height: 190px;" src="./assets/scissors.png" alt=""></p>
        <p v-else-if="player == 'love'"><img style="margin-top: 10px; margin-left: 150px; height: 180px;" src="./assets/love.png" alt=""></p>
      </div>

    
    </div>

    <div>
      <!-- เริ่มเกมใหม่ และ กดเริ่มเล่น -->
      <p style="font-size: x-large;">Result: {{ result }}</p>
      <br>
      <button @click="startGame" :disabled="!player" style="font-size: larger;">Play!!</button>
      <br>
      <p style="font-size: larger; margin-top: 20px;" >AI : {{ ai_point }} Player : {{ player_point }} Draw : {{ tie_point }}</p>
      <br>
      <button @click="reset" style="margin-top: 10px;">Reset</button>
    </div>
  </div>

  

</template>

<style>
template {
  margin: 0;
  display: flex;
  place-items: center;
  min-width: 320px;
  min-height: 100vh;
}

.picture-ai-player {
  display: flex;
  width: 50%;
  margin-left: 220px;
}



</style>