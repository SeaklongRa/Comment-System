<template>
  <div>
    <span>{{ comment.author }}</span>
    <span>3 hours ago</span>
    <blockquote v-text="comment.text"></blockquote>
    <div>
      <v-btn @click="clickReply()">{{ replyText }}</v-btn>
      <v-btn v-show="comment.replies.length" @click="toggleGroup()">{{ toggleText }}</v-btn>
    </div>
    <div class="ml-5" v-show="comment.replies.length && !isGroupRolledUp">
      <comment-nested v-for="reply in comment.replies" :key="reply.id" v-bind:comment="reply" @event_child="emit"></comment-nested>
    </div>
    <div>
      <add-comment
        ref="form"
        v-show="isReplying"
        :comment="comment"
        @text="changeText"
        @addComment="addComment" />
    </div>
  </div>
</template>

<script>
import addComment from './addComment.vue';
export default {
  components: { addComment },
  name: 'comment-nested',

  props: ['comment'],

  methods: {
    toggleGroup: function() {
      this.isGroupRolledUp = !this.isGroupRolledUp;
    },
    clickReply: function() {
      this.isReplying = !this.isReplying;
      if (this.isReplying) {
        var self = this;
        setTimeout(function() {
          self.$refs.form.$refs.input.focus();
        }, 0);
      }
    },
    emit: function(data) {
      this.$emit('event_child', data);
    },
    addComment: function(text) {
      this.isReplying = false;
      this.isGroupRolledUp = false;
      this.$emit('event_child', {
        parent_id: this.comment.id,
        text: text
      });
      console.log(this.comment.id, 'check id')
    },
    changeText: function(data) {
      this.commentText = data;
      console.log(data, 'check data')
    },
  },

  computed: {
    replyText: function() {
      if (this.isReplying) {
        return 'cancel reply';
      } else {
        return 'reply';
      }
    },
    toggleText: function() {
      if (this.isGroupRolledUp) {
        return 'expand';
      } else {
        return 'collapse';
      }
    },
  },

  data: () => ({
    isGroupRolledUp: true,
    isReplying: false,
    commentText: ''
  })

}
</script>

<style>

</style>