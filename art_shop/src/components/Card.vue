<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div :class="[card.sold ? 'card_sold' : '', 'card__container']" ref="card">
    <img :src="card.imgUrl" :alt="card.title" />
    <h2 class="name" v-html="card.title"></h2>
    <div class="cost-block">
      <div class="cost">
        <p class="old-cost">{{ card.oldCost }}</p>
        <p class="cur-cost">{{ card.currentCost }}</p>
        <p class="sold" :style="[card.sold ? '' : 'display:none']">
          Продана на аукционе
        </p>
      </div>

      <BuyButton :card="card"></BuyButton>
    </div>
  </div>
</template>

<script>
import BuyButton from "./buy_button.vue";
export default {
  props: ["card"],

  components: { BuyButton },
};
</script>

<style>
.card {
  margin: 5% 0 5% 0;
  cursor: pointer;
}

.card_sold {
  opacity: 50%;
}
.name,
.cost-block {
  display: flex;
  width: 90%;
}

img {
  width: 100%;
}

.name {
  font-size: 18px;
  font-weight: 400;
  margin: 10% 0 10% 0;
}

.cost-block {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10%;
}

.cost {
  display: flex;
  flex-direction: column;
}

.cur-cost,
.sold {
  font-size: 16px;
  font-weight: bold;
}

.cur-cost,
.old-cost {
  margin: 0;
}

.old-cost {
  color: #a0a0a0;
  text-decoration: line-through;
  font-weight: lighter;
  font-size: 14px;
}

.sold {
  margin-bottom: 15px;
  font-size: 16px;
  font-weight: bold;
}
</style>
