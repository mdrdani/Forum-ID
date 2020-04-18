<template>
  <v-container>
    <v-row justify="center" no-gutters>
      <v-col class="pa-2" cols="12" sm="6">
        <v-card class="pa-md-4 mx-lg-auto" color="white" width="600px">
          <v-form @submit.prevent="submit">
            <v-text-field label="Category Name" v-model="form.name" required></v-text-field>

            <v-btn type="submit" color="orange" v-if="editSlug">Update</v-btn>
            <v-btn type="submit" color="teal" v-else>Create</v-btn>
          </v-form>
        </v-card>
      </v-col>

      <v-col class="pa-2" cols="12" sm="6">
        <v-card class="mx-lg-auto" width="500px" tile>
          <v-list>
            <v-subheader class="title">Category</v-subheader>
            <div v-for="(category,index) in categories" :key="category.id">
              <v-list-item>
                <v-list-item-icon>
                  <v-icon>fas fa-bookmark</v-icon>
                </v-list-item-icon>
                <v-list-item-content>
                  <v-list-item-title>{{category.name}}</v-list-item-title>
                </v-list-item-content>

                <v-list-item-icon>
                  <v-btn small @click="edit(index)">
                    <v-icon color="orange">far fa-edit</v-icon>
                  </v-btn>
                </v-list-item-icon>

                <v-list-item-icon>
                  <v-btn small @click="destroy(category.slug,index)">
                    <v-icon color="red">far fa-trash-alt</v-icon>
                  </v-btn>
                </v-list-item-icon>
              </v-list-item>
            </div>
          </v-list>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: null
      },
      categories: {},
      editSlug: null
    };
  },
  created(){
    if(!User.admin()){
        this.$router.push('/forum')
      }
  },
  mounted(){
    this.load()
  },
  methods: {
    load(){
      axios.get("/api/category").then(res => (this.categories = res.data.data));
    },
    submit() {
       this.editSlug ? this.update() :  this.create();
    },
    update(){
      axios
        .patch(`/api/category/${this.editSlug}`, this.form)
        .then(res => {
          this.load()
          this.form.name = null;
        })
    },
    create() {
      axios
        .post("/api/category", this.form)
        .then(res => {
          this.load()
          this.form.name = null;
        })
        .catch(error => (this.errors = error.response.data.errors));
    },
    edit(index){
      this.form.name = this.categories[index].name
      this.editSlug = this.categories[index].slug
      this.categories.splice(index,1)
    },
    destroy(slug, index) {
      axios
        .delete(`/api/category/${slug}`)
        .then(res => this.categories.splice(index, 1));
    }
  },
  computed: {
    disabled() {
      return !this.form.name;
    }
  }
};
</script>