<template>
  <div>
    <v-text-field label="Comment" v-model="content"></v-text-field>
    <v-btn v-if="$listeners['cancel']" @click="$emit('cancel')">Cancel</v-btn>
    <v-btn @click="$emit('send', content)">{{ label }}</v-btn>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      required: false,
      type: String,
      default: "Send"
    }
  },
  data: () => ({
    content: ""
  })
}
</script>

<style>

</style>