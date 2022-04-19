<template>
  <nav class="pro-filter">
    <button @click="updateFilter('all')" 
    :class="{active:current === 'all'}"
    > view all </button>
    <button @click="updateFilter('completed')"
    :class="{active:current === 'completed'}"

    > Completed</button>
    <button @click="updateFilter('ongoing')"
    :class="{active:current === 'ongoing'}"

    > ongoing </button>
    <button @click="updateFilter('important')"
    :class="{active:current === 'important'}"

    > Important </button>

  </nav>
</template>

<script>
export default {
  props:['current'],
    methods:{
      updateFilter(by){
        this.$emit("filterChange", by)
      }
    }
}
</script>
<style lang="scss" >
// nav {
//   padding: 30px;

//   a {
//     font-weight: bold;
//     color: #2c3e50;

//     &.router-link-exact-active {
//       color: #42b983;
//     }
//   }
// }
button{
    margin: 10px 15px;
    background: #00ce89f2;
    color: #000;
    padding: 10px;
    border: 0;
    border-radius: 7px;
    font-size: 18px;
    font-weight: bold;
    cursor: pointer;
    opacity: .7;

}
    .active,
    button:hover{
    opacity: 1;
    transition: 0.2s cubic-bezier(0.85, 1.43, 0.97, 1.35);
    background: #ff3414;
    color: #f1f1f1;

    }

</style>