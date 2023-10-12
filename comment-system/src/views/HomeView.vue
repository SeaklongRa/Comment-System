<template>
  <v-container>
    <h1>Hello</h1>
    <comment-input />
  </v-container>
</template>

<script>
import CommentInput from '../components/comments/comment-input.vue'

  export default {
    name: 'HomePage',

    components: {
      CommentInput
    },
  }
</script>
