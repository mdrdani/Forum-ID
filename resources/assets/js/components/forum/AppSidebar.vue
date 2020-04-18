<template>
  <v-card class="mx-auto" max-width="500" tile>
    <v-list shaped>
      <v-subheader class="headline">Categories</v-subheader>
      <v-list-item-group color="primary">
        <v-list-item v-for="cat in categories" :key="cat.id">
          <v-list-item-icon>
            <v-icon>fas fa-check-circle</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>{{cat.name}}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>
  </v-card>
</template>

<script>
export default {
    data(){
        return {
            categories: {},
        }
    },
    created(){
        axios.get('/api/category')
        .then(res => this.categories = res.data.data)
    }
};
</script>