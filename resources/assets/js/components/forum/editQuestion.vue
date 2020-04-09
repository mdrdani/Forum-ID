<template>
        <v-container>
            <v-form @submit.prevent="update">
                <v-text-field v-model="form.title" label="Title" type="text" required></v-text-field>
                <vue-simplemde v-model="form.body" ref="markdownEditor" />
                <v-card-actions>
                    <v-btn color="green" type="submit">Save</v-btn>
                    <v-btn color="red" @click="cancel"
                    >Cancel
                    </v-btn>
                </v-card-actions>

            </v-form>
        </v-container>

</template>

<script>
export default {
    props: ['data'],
    data(){
        return{
            form: {
                title : null,
                body : null,
            }
        }
    },
    created(){
        this.form = this.data
    },
    methods: {
        cancel(){
            EventBus.$emit('cancelEditing')
        },
        update(){
            axios.patch(`/api/question/${this.form.slug}`, this.form)
            .then(res => this.cancel())
        }
    }
}
</script>

<style lang="">
    
</style>