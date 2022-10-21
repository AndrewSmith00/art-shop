<template>
  <button
    :class="[
      card.inBasket ? 'button_in-basket' : '',
      card.processed ? 'button_processed' : '',
      'button',
    ]"
    :style="[card.sold ? 'display:none' : '']"
  >
    {{ card.buttonText }}
  </button>
</template>

<script>
export default {
  props: ["card"],
};
</script>

<style>
.button {
  width: 118px;
  height: 48px;
  border: none;
  margin: 0;
  color: white;
  font-weight: bold;
  background-color: #165225;
  cursor: pointer;
}

.button_in-basket {
  background-color: rgb(41, 102, 41);
}

.button_processed {
  background-color: #776763;
}

.button:hover {
  background-color: #776763;
}
</style>
