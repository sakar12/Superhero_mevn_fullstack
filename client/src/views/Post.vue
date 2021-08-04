<template>
  <v-container fluid>
    <v-row no-gutters>
      <v-col sm="10" class="pa-4 mx-auto">
        <v-card class="pa-2">
          <v-img :src="`/${post.image}`"></v-img>
          <v-card-actions class="pb-0">
            <v-row class="mt-1 mx-1">
              <v-col sm="2">
                <v-btn
                  v-if="post.category === 'Marvel'"
                  class="ml-n2 mt-3"
                  small
                  outlined
                  color="red"
                >
                  {{ post.category }}
                </v-btn>
                <v-btn v-else class="ml-n2 mt-3" small outlined color="black">
                  {{ post.category }}
                </v-btn>
              </v-col>
              <v-col sm="10" class="d-flex justify-end">
                <v-btn
                  color="success"
                  :to="{ name: 'edit-post', params: { id: post._id } }"
                  text
                  >Edit</v-btn
                >
                <v-btn color="error" text @click="removePost(post._id)"
                  >Delete</v-btn
                >
              </v-col>
            </v-row>
          </v-card-actions>
          <v-card-subtitle class="headline">
            <h3>{{ post.title }}</h3>
          </v-card-subtitle>
          <v-card-text class="grey--text">
            <p style="color: black">{{ post.content }}</p>
            <p>Posted on: {{ post.created | formatDate }}</p>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import API from "../api";

export default {
  data() {
    return {
      post: {},
    };
  },
  async created() {
    const response = await API.getPostByID(this.$route.params.id);
    this.post = response;

    
  },
  methods: {
    async removePost(id) {
      const response = await API.deletePost(id);
      this.$router.push({
        name: "home",
        params: { message: response.message },
      });
    },

  },
};
</script>
<style scoped>
#editBtn {
  color: white;
  background-color: green;
}

#deleteBtn {
  color: white;
  background-color: red;
}
</style>
