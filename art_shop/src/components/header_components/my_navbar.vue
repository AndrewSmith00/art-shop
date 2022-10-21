<template>
    <ul>
        <li v-for="(item, i) in items" v-bind:key="i">
            <a :href="item.link">{{item.text}}</a>
        </li>
    </ul>
</template>

<script>
    export default {
        props: ["items"]
    }
</script>

<style>
.nav-panel {
  align-self: center;
  list-style-type: none;
  padding: 0 100px 0 0;
}

.nav-panel > li {
  display: inline;
  padding: 0 10px 0 10px;
}
</style>