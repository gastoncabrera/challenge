<!-- Please remove this file from your project -->
<template>
  <div>
    test
    <form @submit.prevent="handleSubmit">
      <input type="text" v-model="title" />
      <input type="text" v-model="description" />
      <button type="submit">{{ !id ? "Enviar" : "Editar" }}</button>
    </form>
    <div v-for="(item, index) in data" :key="index">
      <ul>
        <li>
          {{ item.id }}--{{ item.title }}--{{ item.description }}
          <button @click="deletedata(item.id)">Eliminar</button>
          <button @click="test(item)">Editar</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [],
      id: "",
      title: "",
      description: "",
    };
  },

  methods: {
    async postdata() {
      try {
        await this.$fire.firestore.collection("task").add({
          title: this.title,
          description: this.description,
        });
        this.getdata();
      } catch (error) {
        console.log(error);
      }
    },

    async getdata() {
      try {
        this.data = [];
        const data = await this.$fire.firestore
          .collection("task")
          .get()
          .then((res) => {
            res.forEach((x) => {
              this.data.push({ id: x.id, ...x.data() });
            });
          });
      } catch (error) {
        console.log(error);
      }
    },

    async deletedata(id) {
      try {
        await this.$fire.firestore
          .collection("task")
          .doc(id)
          .delete()
          .then(() => {
            this.getdata();
          });
      } catch (error) {
        console.log(error);
      }
    },
    handleReset() {
      this.title = "";
      this.description = "";
      this.id = "";
    },

    handleSubmit() {
      if (this.id) {
        this.updatedata();
      } else {
        this.postdata();
      }
      this.handleReset();
    },

    test(item) {
      this.title = item.title;
      this.description = item.description;
      this.id = item.id;
    },

    async updatedata() {
      try {
        await this.$fire.firestore
          .collection("task")
          .doc(this.id)
          .set({
            title: this.title,
            description: this.description,
          })
          .then(() => {
            this.getdata();
          });
      } catch (error) {
        console.log(error);
      }
    },
  },
  mounted() {
    this.getdata();
  },
};
</script>
