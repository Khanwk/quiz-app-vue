<template>
  <div className="timmer">
    <p className="no">{{ timer }}</p>
    <p className="sec">sec</p>
  </div>
</template>
<script>
export default {
  name: "Timer",
  props: ["timer"],
};
</script>
<style scoped>
.timmer {
  width: 120px;
  height: 120px;
  position: absolute;
  top: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  border: 10px;
  border-color: rgb(0, 130, 31);
  border-radius: 200px;
  border-style: solid;
  margin: 16px;
  color: rgb(0, 130, 31);
}
.no {
  font-weight: bold;
  font-size: 30px;
  margin: 0;
  font-family: "Jost";
}
.sec {
  font-weight: bold;
  font-size: 20px;
  margin: 0;
  font-family: "Jost";
}
</style>
