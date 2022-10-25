<template>
  <div class="opened-card">
    <div class="opened-card__header">
      <h2 class="row">Информация о товаре</h2>
      <div
        id="closeButton"
        class="close-button"
        v-on:click="this.$emit('buttonClick', card.id, $event)"
      >
        &#215;
      </div>
    </div>

    <div class="gallery row">
      <div class="large-img-container row">
        <img class="large-img" :src="largeImage" alt="" />
      </div>


      <ul class="thumbs row">
        <li
          class="img-container col-xs-3"
          v-for="(img, i) in imgs"
          v-bind:key="i"
        >
          <img
            class="thumb-img"
            v-on:click="swapImages(i)"
            :src="imgs[i].small"
            alt=""
          />
        </li>
      </ul>
    </div>
    <div class="opened-card__info column">
      <div class="name" v-html="card.title"></div>
      <div class="cost-block">
        <p class="old-cost">{{ card.oldCost }}</p>
        <p class="cur-cost">{{ card.currentCost }}</p>
        <p class="sold-message" :style="[card.sold ? '' : 'display:none']">
          Продана на аукционе
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["card"],

  data() {
    return {
      isOpen: true,
      largeImage:
        this.card.imgUrl + this.card.name + "/" + this.card.name + ".png",
      imgs: {
        0: {
          large:
            this.card.imgUrl + this.card.name + "/" + this.card.name + ".png",
          small:
            this.card.imgUrl +
            this.card.name +
            "/" +
            this.card.name +
            "-thumb.png",
        },
        1: {
          large: this.card.imgUrl + this.card.name + "/1.png",
          small: this.card.imgUrl + this.card.name + "/1-thumb.png",
        },
        2: {
          large: this.card.imgUrl + this.card.name + "/2.png",
          small: this.card.imgUrl + this.card.name + "/2-thumb.png",
        },
        3: {
          large: this.card.imgUrl + this.card.name + "/3.png",
          small: this.card.imgUrl + this.card.name + "/3-thumb.png",
        },
      },
    };
  },

  methods: {
    /*closeCard() {
        this.$emit('closeCard');
    },*/
    swapImages(imageNumber) {
      this.largeImage = this.imgs[imageNumber].large;
    },
    buttonClick(cardId, event) {
      this.$emit("buttonClick", cardId, event);
    },
  },
};
</script>

<style>
.opened-card {
  position: fixed;
  top: 15%;
  left: 20%;
  width: 50%;
  height: 70%;
  padding: 0 5% 0 5%;
  display: flex;
  justify-content: center;
  flex-direction: column;
  background-color: #fff;
  border: 2px solid #9f9f9f;
  z-index: 2;
}

.opened-card__header {
  display: flex;
  justify-content: space-between;
}

.opened-card__info {
  display: flex;
  justify-content: space-between;
}

.close-button {
  justify-self: flex-end;
  width: fit-content;
  height: fit-content;
  padding: 0 4px 0 4px;
  cursor: pointer;
  background-color: #b80808;
  border: 2px solid black;
  color: #fff;
  font-weight: bold;
}

.gallery {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 100%;
}

.large-img-container {
  display: flex;
  width: 100%;
  justify-content: center;
  align-items: center;
}

.thumbs {
  padding: 0;
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.img-container {
  list-style: none;
}

@media screen and (max-width: 976px) {
  .opened-card {
    top: 15%;
    left: 5%;
    width: 80%;
  }
}

@media screen and (max-width: 700px) {
  .thumb-img {
    width: 70px;
  }
}

@media screen and (max-width: 480px) {
  .large-img {
    height: 120px;
  }
  .thumb-img {
    width: 40px;
  }
}

@media screen and (max-width: 310px) {
  .large-img {
    height: 80px;
  }
  .thumb-img {
    width: 25px;
  }
}
</style>
