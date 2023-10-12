<template>
  <div>
    <div>
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
    }
  },
  data: () => ({
    replying: false
  })
}
</script>

<style>

</style>