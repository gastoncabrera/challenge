<template>
  <v-card class="card" max-width="344" min-width="200">
    <v-list-item three-line>
      <v-list-item-content>
        <div class="text-overline card__title">
          {{ data.title }}
          <!-- -------------------- -->

          <div data-app>
            <v-row justify="center">
              <v-dialog v-model="dialog" persistent max-width="600px">
                <template v-slot:activator="{ on, attrs }">
                  <v-icon
                    small
                    color="#0000ff"
                    @click="test(data)"
                    v-bind="attrs"
                    v-on="on"
                    >mdi-pencil</v-icon
                  >

                  <!-- ---------------------------- -->
                </template>
                <v-card>
                  <v-card-title>
                    <span class="text-h5">Edit task</span>
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
                  <v-card-actions class="actions__button">
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
        <v-list-item-title class="text-h5">{{
          data.description
        }}</v-list-item-title>
      </v-list-item-content>
    </v-list-item>
    <v-card-actions>
      <v-btn
        class="card__button"
        :color="data.isComplete ? `#4caf50` : `#ff5252`"
        outlined
        text
        @click="updatecomplete(data)"
        >{{ data.isComplete ? "completar" : "completado" }}</v-btn
      >
      <v-btn @click="deletedata(data.id)" color="#ff0000" outlined text
        >Delete</v-btn
      >
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  props: {
    data: Object,
    getdata: {
      type: Function,
    },
  },

  data() {
    return {
      dialog: false,
      id: "",
      title: "",
      description: "",
    };
  },

  methods: {
    handleSubmit() {
      this.updatedata();
      this.handleReset();
    },

    handleReset() {
      this.id = "";
      this.title = "";
      this.description = "";
      this.dialog = false;
    },

    test(item) {
      this.id = item.id;
      this.title = item.title;
      this.description = item.description;
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

    async updatecomplete(data) {
      try {
        await this.$fire.firestore
          .collection("task")
          .doc(data.id)
          .set({
            ...data,
            isComplete: !data.isComplete,
          })
          .then(() => {
            this.getdata();
          });
      } catch (error) {
        console.log(error);
      }
    },

    async deletedata(id) {
      try {
        await this.$fire.firestore.collection("task").doc(id).delete();
        this.getdata();
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style scoped>
.card {
  margin: 10px;
}
.card__title {
  display: flex;
  justify-content: space-between;
}

.card__button {
  margin-right: auto;
}

.actions__button {
  flex-wrap: nowrap;
}
</style>