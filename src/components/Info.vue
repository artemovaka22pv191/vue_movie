<template>
  <div class="t">
    <b-container class="info">
      <b-row><p class="lead my-2 text-danger fs-6">A-tear - высшая категория, то, что реально можно назвать
        искусством</p></b-row>
      <b-row><p class="lead my-2 text-success fs-6">В-tear - первый сорт. Частенько может попасться что-то
        интересное</p></b-row>
      <b-row><p class="lead my-2 text-warning fs-6">C-tear - второсортное кино, которое люди не в теме и относящиеся
        к этому серьёзно, но, если относиться просто, то порой заходят</p></b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "Info"
}
</script>

<style scoped>
.info {
  margin-top: 5%;
  background: rgba(255, 255, 255, 0.87);
  margin-right: 10%;
}
.t{
  margin-right: 10%;
}
</style>