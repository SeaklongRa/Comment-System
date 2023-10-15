<template>
  <div>
    <comment-body :comment="comment" @send="send" />
    <div>
      <comment-body v-for="reply in replies" :comment="reply" @send="send" :key="reply.id" :countReply="numbers[replies.length - 1]" />
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
    numbers: []
  }),
  methods: {
    send(content) {
      this.replies.push(content)
      console.log('replies', this.replies.length)
      this.numbers.push(20 * this.replies.length)
      console.log(this.numbers[this.replies.length - 1], 'check value')
    }
  }
}
</script>

<style>

</style>