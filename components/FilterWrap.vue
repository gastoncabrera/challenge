<template>
  <v-card height="100%" width="256" class="mx-auto">
    <v-navigation-drawer permanent>
      <v-list-item class="">
        <v-text-field
          label="Search"
          v-model="search"
          persistent-hint
          class=""
        ></v-text-field>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" link>
          <v-list-item-icon>
            <v-icon class="input">{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </v-card>
</template>

<script>
export default {
  props: {
    filter: Object,
  },

  data() {
    return {
      items: [
        { title: "Todos", icon: "mdi-format-list-numbered-rtl" },
        { title: "Completados", icon: "mdi-check-all" },
      ],
      right: null,
      search: "",
    };
  },
  computed: {
    inputfilter() {
      this.filter.search = this.search;
      console.log(this.search);
    },
  },
};
</script>

<style  scoped>
.filter {
  border: 1px solid red;
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
</style>