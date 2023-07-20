<script setup lang="ts">
import { ref } from 'vue'

// refs
const position = ref({ x: 0, y: 0})

// const
const minimumTranslate = 50
const buttonSizePx = 100
const maxWidth = ((window.innerWidth - buttonSizePx) / 2) - minimumTranslate
const maxHeight = ((window.innerHeight - buttonSizePx) / 2) - minimumTranslate
const direction = [1, -1]

// functions
function generateNewPosition() {
  let nextPositionX = generateRandomPosition(maxWidth)
  while((nextPositionX < position.value.x + minimumTranslate && nextPositionX > position.value.x - minimumTranslate)) {
    nextPositionX = generateRandomPosition(maxWidth)
  }
  let nextPositionY = generateRandomPosition(maxHeight)
  while((nextPositionY < position.value.y + minimumTranslate && nextPositionY > position.value.y - minimumTranslate)) {
    nextPositionY = generateRandomPosition(maxHeight)
  }
  position.value = { x: nextPositionX, y: nextPositionY }
}
function generateRandomPosition(maxValue) {
  return (Math.floor(Math.random() * (maxValue - minimumTranslate + 1)) + minimumTranslate) * direction[Math.floor(Math.random() * direction.length)]
}
</script>

<template>
  <div class="main">
    <button @mouseover="generateNewPosition" class="annoying-button" :style="{ 
      transform: 'translateX(' + position.x + 'px) translateY(' + position.y + 'px)',
      width: buttonSizePx + 'px'
      }">Click me</button>
  </div>
</template>

<style scoped>
.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.annoying-button {
  transition: 0.1s;
}
</style>
