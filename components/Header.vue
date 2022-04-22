<template>
  <div class="header">
    <div class="header__container">
      <div class="header__logo">Todo List</div>
      <div data-app>
        <v-row justify="center">
          <v-dialog v-model="dialog" persistent max-width="600px">
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                class="mx-2"
                fab
                dark
                small
                color="#4caf50"
                v-bind="attrs"
                v-on="on"
              >
                <v-icon dark> mdi-plus </v-icon>
              </v-btn>
            </template>
            <v-card>
              <v-card-title>
                <span class="text-h5">"New task"</span>
              </v-card-title>
              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12">
                      <v-text-field
                        v-model="title"
                        label="Title"
                        type="text"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12">
                      <v-textarea
                        v-model="description"
                        label="Description"
                      ></v-textarea>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="handleReset">
                  Close
                </v-btn>
                <v-btn color="blue darken-1" text @click="handleSubmit">
                  Save
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-row>
      </div>
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
  data: () => ({
    dialog: false,
    title: "",
    description: "",
  }),

  computed: {},

  methods: {
    handleSubmit() {
      this.postdata();
      this.handleReset();
    },

    handleReset() {
      this.title = "";
      this.description = "";
      this.dialog = false;
    },

    async postdata() {
      try {
        await this.$fire.firestore.collection("task").add({
          title: this.title,
          description: this.description,
          isComplete: false,
        });
        console.log("submit");
        this.getdata();
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style  scoped>
.header {
  background-color: rgb(23, 23, 23);
  width: 100%;
  height: 100%;
  padding: 30px 0;
}

.header__container {
  padding: 0 40px 0 30px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

@media (min-width: 900px) {
  .header__container {
    padding: 0;

    margin: 0 auto;
    width: 80%;
  }
}

.header__logo {
  color: white;
}
</style>