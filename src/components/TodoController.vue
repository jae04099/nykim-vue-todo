<template>
  <div class="controller">
    <div class="select">
      <label for="order" class="blind">Order</label>
      <select name="order" id="order" class="selectbox" v-model="selected" @change="sortTodo">
          <option value="date-asc">Oldest</option>
          <option value="date-desc">Latest</option>
      </select>
    </div>
    <button class="clear" @click="clearTodo">Clear All</button>
  </div>
</template>
<script>
export default {
    data(){
        return {
            selected: "date-asc"
        }
    },
    methods: {
       sortTodo(){
           this.$emit("sortItem", {value: this.selected});
       },
       clearTodo(){
           this.$emit("removeAll")
       }
    }
}
</script>
<style lang="scss">
.controller {
  max-width: $max-width;
  margin: 0 auto;
  @include flexbox;
  @include align-items(center);
  @include justify-content(space-between);
  .clear {
    letter-spacing: 0.014rem;
    font-size: 1.4rem;
    color: #ababab;
    transition: color 0.2s;
    &:hover {
      color: #8e8e8e;
    }
  }
}
.selectbox {
  display: block;
  width: 9.2rem;
  height: 3rem;
  padding: 0.5rem 1rem;
  font-size: 1.4rem;
  color: #747474;
  border: solid 1px #cbcbcb;
  background-color: #ffffff;
  -webkit-appearance: none;
  -moz-appearance: none;
  border-radius: 0;
  outline: 0;
  background-position: right 0.8rem top 55%;
  background-size: 1.15rem 1.15rem;
  background-image: icon("tri", "717171");
  background-repeat: no-repeat;
  cursor: pointer;
  transition: border 0.2s;
  &:hover {
    border-color: #a9a9a9;
  }
}
</style>