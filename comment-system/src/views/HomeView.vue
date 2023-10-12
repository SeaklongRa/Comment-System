<template>
  <v-container>
    <h1>Hello</h1>
    <comment-section :comments="comments" @send="send" />
  </v-container>
</template>

<script>
import CommentSection from '../components/comments/comment-section.vue'

  export default {
    name: 'HomePage',

    components: {
      CommentSection
    },
    methods: {
      send (content) {
        this.comments.push(content)
      }
    },
    data: () => ({
      comments: [
      ]
    })
  }
</script>
