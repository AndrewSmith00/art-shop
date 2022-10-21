<template>
  <body>
    <header class="header">
      <Dropdown class="dropdown" :items="navbarItems" />
      <Navbar :items="navbarItems" class="nav-panel"/>
      <form action="search" onsubmit="return false;" class="search-form">
        <input
          type="text"
          onfocus="this.placeholder=''"
          class="search-input"
          placeholder="Поиск по названию картины"
          v-model="search"
        />
      </form>
    </header>

    <main class="container">
      <h1 class="main-header">Картины эпохи Возрождения</h1>
      <div class="cards">
        <div class="row">
          <div
            class="card card_noPadding col-xs-12 col-md-6 col-xl-3"
            v-for="card in filteredCards"
            v-bind:key="card.id"
            v-on:click="handleClick(card.id, $event)"
          >
            <card :card="card"></card>
          </div>
        </div>
      </div>
    </main>

    <Footer :navbarItems="navbarItems"></Footer>
  </body>
</template>

<script>
import Card from "./components/Card.vue";
import Dropdown from "./components/header_components/my_dropdown.vue";
import Navbar from "./components/header_components/my_navbar.vue"
import Footer from "./components/my_footer.vue"
export default {
  name: "App",
  components: {
    Card,
    Dropdown,
    Navbar, 
    Footer
  },
  data() {
    return {
      search: "",
      basket: {
        0: false,
        1: false,
        2: false,
        3: false,
        4: false,
      },

      navbarItems: [
        {
          text: "Каталог",
          link: "#",
        },
        {
          text: "Доставка",
          link: "#",
        },
        {
          text: "Оплата",
          link: "#",
        },
        {
          text: "Контакты",
          link: "#",
        },
        {
          text: "О компании",
          link: "#",
        },
      ],

      cards: [
        {
          id: "0",
          imgUrl: "./static/imgs/venus.png",
          title: "«Рождение Венеры» <br> Сандро Боттичелли",
          currentCost: "1 000 000 $",
          oldCost: "2 000 000 $",
          buttonText: "Купить",
          inBasket: false,
          sold: false,
          processed: false,
        },
        {
          id: "1",
          imgUrl: "./static/imgs/supper.png",
          title: "«Тайная вечеря» <br> Леонардо да Винчи",
          currentCost: "3 000 000 $",
          oldCost: null,
          buttonText: "Купить",
          inBasket: false,
          sold: false,
          processed: false,
        },
        {
          id: "2",
          imgUrl: "./static/imgs/adam.png",
          title: "«Сотворение Адама» <br> Микеланджело",
          currentCost: "5 000 000 $",
          oldCost: "6 000 000 $",
          buttonText: "Купить",
          inBasket: false,
          sold: false,
          processed: false,
        },
        {
          id: "3",
          imgUrl: "./static/imgs/anatomy.png",
          title: "«Урок анатомии» <br> Рембрандт",
          currentCost: null,
          oldCost: null,
          buttonText: "Купить",
          inBasket: false,
          sold: true,
          processed: false,
        },
      ],
    };
  },

  methods: {
    addToBasket(cardId) {
      this.cards[cardId].processed = true;
      this.cards[cardId].buttonText = "Ожидание...";

      if (this.basket[cardId] == false) {
        setTimeout(() => {
          this.basket[cardId] = true;
          localStorage.setItem("basket", JSON.stringify(this.basket));

          this.cards[cardId].inBasket = true;
          this.cards[cardId].processed = false;
          this.cards[cardId].buttonText = "\u2713 В корзине";
        }, 1000);
      } else {
        setTimeout(() => {
          this.basket[cardId] = false;
          this.cards[cardId].buttonText = "Купить";
          localStorage.setItem("basket", JSON.stringify(this.basket));
          this.cards[cardId].inBasket = false;
          this.cards[cardId].processed = false;
        }, 1000);
      }
    },

    handleClick: function (cardId, event) {
      if (event.target.tagName === "BUTTON") {
        this.addToBasket(cardId);
      }
    },
  },

  computed: {
    filteredCards() {
      return this.cards.filter((card) =>
        card.title.toLocaleLowerCase().includes(this.search.toLocaleLowerCase())
      );
    },
  },

  mounted() {
    let basket = localStorage.getItem("basket");

    if (basket !== null) {
      this.basket = JSON.parse(basket);
    }

    for (let i = 0; i < 5; i++) {
      if (this.basket[i] == true) {
        this.cards[i].buttonText = "\u2713 В корзине";
        this.cards[i].inBasket = true;
      } else {
        this.cards[i].buttonText = "Купить";
      }
    }
  },
};
</script>

<style>
@import "https://unpkg.com/flexboxgrid2@7.2.1/flexboxgrid2.min.css";

html,
body {
  margin: 0;
  min-height: 100vh;
}

body {
  display: flex;
  flex-direction: column;
  font-style: merriweather;
  color: #343030;
}

header,
footer {
  flex: none;
}

main {
  -webkit-overflow-scrolling: touch;
  flex: auto;
}

a {
  text-decoration: none;
  color: #343030;
  cursor: pointer;
}

/* ----------------------------------- Header --------------------------------- */

.header {
  display: flex;
  justify-content: space-around;
  align-items: center;
  height: 97px;
  border-bottom: 1px solid #e1e1e1;
}

/* --------------------------------- Search form ------------------------------ */

.search-form {
  display: flex;
  font-size: 14px;
  width: 30%;
}

.search-input {
  height: 42px;
  width: 100%;
  color: #9f9f9f;
  margin: 0;
}

.search-input {
  border: 2px solid #9f9f9f;
  font-family: "Helvetica";
  font-size: 18px;
}

/* ------------------------------ main block -------------*/

.main-header {
    margin: 54px 0 0 0;
    font-size: 24px;
    font-weight: bold;
}

.container {
    height: 100%;
    display: flex;
    flex-direction: column;
}



.card__container {
    display: flex;
    flex-direction: column;

    align-items: center;
    border: 1px solid #E1E1E1;
}
</style>
