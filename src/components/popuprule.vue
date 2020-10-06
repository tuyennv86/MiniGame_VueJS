<template>
  <div class="wrapper-popup" v-bind:class="{ 'open-pop': isOpenpopup == true }">
    <div class="rule">
      <h3>Luật chơi</h3>
      <p>
        Lorem ipsum, dolor sit amet consectetur adipisicing elit. Maiores
        doloremque cumque esse beatae repellat, accusantium nemo enim pariatur
        veritatis dicta! Repellat ratione quibusdam expedita velit corporis
        itaque rem, repudiandae minima.
      </p>
      <button v-on:click="xacnhan">Đã hiểu</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "popuprule",
  data() {
    return {};
  },
  methods: {
    xacnhan() {
      this.$emit("confirm");
    }
  },
  props: {
    isOpenpopup: {
      type: Boolean,
      default: false,
    }
  },
};
</script>

<style>
.wrapper-popup {
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 2;
  transform: all 0.3s ease;
  opacity: 0;
  visibility: hidden;
}
.open-pop {
  opacity: 1 !important;
  visibility: visible;
}
.rule {
  background: #ffffff;
  position: absolute;
  top: 30%;
  left: 50%;
  width: 400px;
  transform: translate(-50%, -50%);
  font-family: Arial, Helvetica, sans-serif;
  padding: 30px 30px;
  transform: all 0.3s ease;
}
.rule h3 {
  padding-bottom: 10px;
}
.rule button {
  padding: 5px 15px;
  border: 1px solid #ddd;
  background-color: #ddd;
  margin-top: 20px;
  font-weight: 600;
}
.rule button:hover {
  color: salmon;
}
</style>
