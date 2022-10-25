<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div :class="[card.sold ? 'card_sold' : '', 'card__container']" ref="card">
    <img
      class="card__img"
      :src="card.imgUrl + card.name + '/' + card.name + '.png'"
      :alt="card.title"
    />
    <h2 class="card__name" v-html="card.title"></h2>
    <div class="card__cost-block">
      <div class="cost">
        <p class="old-cost">{{ card.oldCost }}</p>
        <p class="cur-cost">{{ card.currentCost }}</p>
        <p class="soldMessage" :style="[card.sold ? '' : 'display:none']">
          Продана на аукционе
        </p>
      </div>

      <BuyButton :card="card"></BuyButton>
    </div>
  </div>
</template>

<script>
import BuyButton from "./BuyButton.vue";
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

.card__name,
.card__cost-block {
  display: flex;
  width: 90%;
}

.card__img {
  width: 100%;
}

.card__name {
  font-size: 18px;
  font-weight: 400;
  margin: 10% 0 10% 0;
}

.card__cost-block {
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
.soldMessage {
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

.soldMessage {
  margin-bottom: 15px;
  font-size: 16px;
  font-weight: bold;
}
</style>
