<template>
  <footer class="footer">
    <Navbar :items="navbarItems" class="nav-panel footer__nav-panel" />

    <div class="footer__contacts">
      <p class="phone-number">+7 (812) 555-55-55</p>
      <p class="address">г. Санкт-Петербург, ул. Ефимова, 3</p>
    </div>
  </footer>
</template>

<script>
import Navbar from "./header_components/NavBar.vue";

export default {
  props: ["navbarItems"],
  components: { Navbar },
};
</script>

<style>
.footer {
  position: relative;
  bottom: 0;
  left: 0;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 96px;
  border-top: 1px solid #e1e1e1;
  background-color: #eceaea;
}

.footer__nav-panel {
  display: flex;
}

.footer__contacts {
  padding-bottom: 0px;
}



@media screen and (max-width: 940px) {
  .footer {
    flex-direction: column;
    height: fit-content;
    margin-top: 20px;
  }

  .footer__nav-panel {
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 0;
  }

  .footer__nav-panel > li {
    display: flex;
    justify-self: center;
    padding-top: 15px;
    padding-bottom: 5px;
    font-size: 20px;
  }

  .footer__contacts {
    font-size: 20px;
    padding-bottom: 30px;
  }

  .phone-number {
    text-align: center;
  }
}
</style>
