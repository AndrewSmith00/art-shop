<template>
  <p @click="isOpen = !isOpen">Развернуть</p>

</template>

<script>
export default {
  isOpen: false,
  props: ["items"],
};
</script>

<style>
.dropdown {
  display: none;
  background-color: white;
  height: 44px;
  width: 20%;
  min-width: fit-content;
  cursor: pointer;
  border: 2px solid #9f9f9f;
  font-family: "Helvetica";
  font-size: 18px;
}

.dropdown > p {
  padding: 0;
  margin: 0;
}

.dropdown:hover {
  background-color: #d8d4d3;
}

@media screen and (max-width: 940px) {
  .nav-panel {
    display: none;
  }

  .dropdown {
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
</style>
