<template>
  <div class="dropdown" @click="isOpen = !isOpen">
    <p >Развернуть</p>
    <transition name="fade" appear>
      <div class="dropdown__navbar" v-if="isOpen">
        <div class="navbar__element" v-for="(item, i) in items" v-bind:key="i">
          <a :href="item.link">{{ item.text }}</a>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: ["items"],
  data() {
    return {
      isOpen: false,
    };
  },
};
</script>

<style>
.dropdown {
  display: none;
  background-color: fff;
  height: 44px;
  min-width: 20%;
  cursor: pointer;
  border: 2px solid #9f9f9f;
  font-family: "Helvetica";
  font-size: 18px;
}

.dropdown:hover {
  background-color: #d8d4d3;
}

.dropdown__navbar {
  min-width: 100%;
  border: 2px solid #9f9f9f;
  background-color: #fff;

}

.fade-enter-actice, 
.fade-leave-active {
  transition: all .5s ease-out;
}

.fade-enter, 
.fade-leave-to {
  opacity: 0;
}

.navbar__element {
  text-align: center;
  padding-top: 7px;
  padding-bottom: 7px;

}

.navbar__element:hover {
  background-color: #d8d4d3;
}

@media screen and (max-width: 940px) {
  .nav-panel {
    display: none;
  }

  .dropdown {
    display: flex;
    flex-direction: column;
    justify-content:flex-start;
    align-items:center;
    position: absolute;
    top: 25px;
    left: 10%
  }
  
  .dropdown p {
    margin-top: 13px;
    padding: 0 10px 0 10px;
  }
}
</style>
