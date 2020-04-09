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
      <v-card-text v-html="body"></v-card-text>
      <v-card-actions v-if="own">
        <v-btn icon @click="edit">
          <v-icon small color="orange">fas fa-pencil-alt</v-icon>
        </v-btn>
        <v-btn icon @click="destroy">
          <v-icon small color="red">fas fa-trash-alt</v-icon>
        </v-btn>
      </v-card-actions>
    </v-container>
  </v-card>
</template>

<script>
export default {
  props: ["data"],
  data(){
    return{
      own : User.own(this.data.user_id)
    }
  },
  computed: {
    body() {
      return md.parse(this.data.body);
    }
  },
  methods: {
    destroy() {
      axios
      .delete(`/api/question/${this.data.slug}`)
      .then(res => this.$router.push('/forum'))
      .catch(error => console.log(error.response.data))
    },
    edit(){
      EventBus.$emit('startEditing')
    }
  }
};
</script>