<template>
  <div>
    <comment-body :comment="comment" @send="send" />
    <div :style="{margin: number + 'px'}">
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
    replies: [],
    number: 0
  }),
  methods: {
    send(content) {
      this.replies.push(content)
      console.log('replies', this.replies)
      this.number += 20
    }
  }
}
</script>

<style>

</style>