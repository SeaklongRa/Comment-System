<template>
  <div>
    <v-text-field
      ref="input"
      label="Reply Comment"
      placeholder="Your comment"
      @input="text"
      v-model="commentText">
    </v-text-field>
    <v-btn @click="addComment">Add</v-btn>
  </div>
</template>

<script>
export default {
  name: 'AddComment',

  props: ['comment'],

  data: () => ({
    commentText: ''
  }),

  methods: {
    addComment: function() {
      if (this.commentText.trim() === '') return false;
      this.$emit('addComment', this.commentText.trim());
      this.commentText = '';
    },
    text: function() {
      this.$emit('text', this.commentText.trim());
    }
  }

}
</script>

<style>

</style>