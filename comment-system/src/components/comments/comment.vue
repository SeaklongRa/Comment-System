<template>
  <div>
    <comment-body :comment="comment" @send="send" />
    <div class="ml-5">
      <comment-body v-for="reply in replies" :comment="reply" @send="send" :key="reply.id" />
    </div>
  </div>
</template>

<script>
import commentBody from './comment-body.vue'
export default {
  components: { commentBody },
  name: 'CommentPage',
  props: {
    comment: {
      required: true,
      type: String
    }
  },
  data: () => ({
    replies: []
  }),
  methods: {
    send(content) {
      this.replies.push(content)
    }
  }
}
</script>

<style>

</style>