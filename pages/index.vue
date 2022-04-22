<template>
  <div>
    <Header :getdata="getdata" />
    <div class="cont">
      <v-text-field
        label="Search"
        v-model="filter.search"
        persistent-hint
        class="cont__search"
      ></v-text-field>
    </div>
    <Main :data="itemFiltered" :getdata="getdata" />
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      data: [],
      filter: {
        search: "",
        complete: false,
      },
    };
  },

  mounted() {
    this.getdata();
  },

  computed: {
    itemFiltered() {
      // let cloneItems = this.data;
      let cloneItems = this.data.filter((item) => {
        if (item.title.toLowerCase().includes(this.filter.search.toLowerCase()))
          return item;
      });
      return cloneItems;
    },
  },

  methods: {
    allItems() {
      this.filter.complete = false;
    },
    IsCompleteItems() {
      this.filter.complete = true;
    },

    async getdata() {
      try {
        this.data = [];
        await this.$fire.firestore
          .collection("task")
          .get()
          .then((res) => {
            res.forEach((x) => {
              this.data.push({ id: x.id, ...x.data() });
            });
          });
        console.log("esto es del get", this.data);
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style scoped>
.filter {
  max-width: 400px;
}

.filter__wrap {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.input {
  margin-right: 20px;
}
.cont {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  padding: 15px 0;
}
@media (min-width: 600px) {
  .cont {
    flex-direction: row;
  }
}
@media (min-width: 900px) {
  .cont {
    margin: 0 auto;
    width: 80%;
  }
}

.cont__search {
  padding: 0 16px;
}
.list {
  display: flex;
  flex-basis: min-content;
}
</style>