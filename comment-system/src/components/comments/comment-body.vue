<template>
  <div>
    <div :style="{margin: countReply + 'px'}">
      <p v-html="comment"></p>
      <v-btn v-if="!replying" @click="replying = true">Reply</v-btn>
    </div>

    <comment-input v-if="replying" @send="(c) => $emit('send', c)" @cancel="replying = false" />
  </div>
</template>

<script>
import commentInput from './comment-input.vue'
export default {
  components: { commentInput },
  props: {
    comment: {
      required: true,
      type: String
    },
    countReply: {
      required: false,
      type: Number,
    }
  },
  data: () => ({
    replying: false,
    numbers: 0
  }),
  computed: {
  }
}
</script>

<style>

</style>