<template>
  <div>
    <h1>เป่า ยิ้ง ฉุบ</h1>
    <button @click="playGame('random')">เป่า ยิ้ง ฉุบ</button>
    <button @click="resetGame">เริ่มใหม่</button> <!-- เพิ่มปุ่ม "เริ่มใหม่" -->
    <img :src="playerImgUrl" alt="Player choice" />
    <img :src="computerImgUrl" alt="Computer choice" />
    <p>{{ result }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const playerImgUrl = ref('src/assets/player.png');
const computerImgUrl = ref('src/assets/player.png');
const result = ref('');

const choices = {
  rock: 'src/assets/rock.png',
  paper: 'src/assets/paper.png',
  scissors: 'src/assets/scissors.png',
  love: 'src/assets/love.png', // เพิ่มตัวเลือกใหม่
};

const playGame = (playerChoice) => {
  if (playerChoice === 'random') {
    playerChoice = ['rock', 'paper', 'scissors', 'love'][Math.floor(Math.random() * 4)]; // เพิ่มตัวเลือกใหม่
  }

  const computerChoice = ['rock', 'paper', 'scissors', 'love'][Math.floor(Math.random() * 4)]; // เพิ่มตัวเลือกใหม่
  playerImgUrl.value = choices[playerChoice];
  computerImgUrl.value = choices[computerChoice];
  
  if (playerChoice === computerChoice) {
    result.value = 'Draw!';
  } else if (
    (playerChoice === 'rock' && computerChoice === 'scissors') ||
    (playerChoice === 'paper' && computerChoice === 'rock') ||
    (playerChoice === 'scissors' && computerChoice === 'paper') ||
    (playerChoice === 'love' && computerChoice !== 'love') // ตัวเลือกใหม่ชนะตัวเลือกอื่นทุกตัว
  ) {
    result.value = 'You win!';
  } else {
    result.value = 'You lose!';
  }
};

const resetGame = () => {
  playerImgUrl.value = 'src/assets/player.png';
  computerImgUrl.value = 'src/assets/player.png';
  result.value = '';
};
</script>
