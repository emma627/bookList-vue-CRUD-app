<template>
  <button :style="{ background: color }" class="btn"
  @click="btnClick">{{ text }}</button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    color: String,
  },
  methods:{
    btnClick(){
      this.$emit("btn-click")
    }
  }
};
</script>

<style>
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 20px;
  font-weight: bold;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}
</style>
