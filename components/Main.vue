<template>
  <div class="main">
    <div class="main__list">
      <Card
        v-for="(item, index) in data"
        :key="index"
        :data="item"
        :getdata="getdata"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    data: Array,

    getdata: {
      type: Function,
    },
  },
};
</script>

<style scoped>
.main {
  margin: 20px 0;
}

.main__list {
  width: 100%;
  flex-direction: row;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  row-gap: 15px;
}
@media (min-width: 500px) {
  .main__list {
    justify-content: left;
  }
}
@media (min-width: 900px) {
  .main__list {
    margin: 0 auto;
    width: 80%;
  }
}
</style>