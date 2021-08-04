<template>
  <v-container>
    <v-row no-gutters>
      <v-col sm="10" class="mx-auto">
        <v-card class="pa-5">
          <v-card-title class="mt-n4 ml-1 mb-n4">Create New Post</v-card-title>
          <v-form ref="form" @submit.prevent="submitForm" class="pa-5" enctype="multipart/form-data">
            <v-text-field
              label="Title"
              append-outer-icon="mdi-note"
              :rules="rules"
              outlined
              v-model="post.title"
            ></v-text-field>
            <v-text-field
              label="Category"
              append-outer-icon="mdi-view-list"
              :rules="rules"
              outlined
              v-model="post.category"
            ></v-text-field>
            <v-textarea
              label="Content"
              append-outer-icon="mdi-note-plus"
              :rules="rules"
              outlined
              v-model="post.content"
            ></v-textarea>
            <v-file-input
            @change="selectFile"
              :rules="rules"
              show-size
              counter
              multiple
              label="Select Image"
              outlined
            ></v-file-input>
            <v-btn type="submit" class="" color="primary">Add Post</v-btn>
          </v-form>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
import API from "../api"
export default {
    data(){
        return{
            rules: [(value)=>!!value || "This field is required!"],
            post : {
            category : "",
            content :"",
            image:"",
            },
            image:"",
        };
    },

    methods: {
        selectFile(file){
            this.image = file[0];
        },
        async submitForm(){
            const formData = new FormData();
            formData.append('image',this.image);
            formData.append('title',this.post.title);
            formData.append('category',this.post.category);
            formData.append('content',this.post.content);
            if(this.$refs.form.validate()) {
                const response = await API.addPost(formData);
                this.$router.push({ name: 'home', params: {message: response.message}});
            }
        },
    }
}
</script>
<style scoped>
.v-file-input {
  flex-direction: row-reverse;
}
</style>