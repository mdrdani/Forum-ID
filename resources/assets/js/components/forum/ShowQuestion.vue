<template>
  <v-card class="ma-3">
    <v-container fluid>
      <v-card-title>
        <div>
          <h3 class="headline">{{data.title}}</h3>
          <h6 class="grey--text">{{data.user}} said {{data.created_at}}</h6>
        </div>
      <v-spacer></v-spacer>
      <v-btn class="teal">5 Replies</v-btn>
      </v-card-title>
      <v-card-text v-html="data.body"></v-card-text>
    </v-container>
  </v-card>
</template>

<script>
export default {
  props: ["data"]
};
</script>