<template>
  <v-container>
    <v-text-field
      label="Comment"
      placeholder="Your comment"
      v-model="commentText">
    </v-text-field>
    <v-btn @click="addComment">Add</v-btn>

    <comment
      v-for="comment in comments"
      :key="comment.id"
      :comment="comment"
      @event_child="eventChild" />

    <!-- <div class="vcomments">
      <div class="vcomments__add-block">
        <input class="vcomments__add-input" placeholder="Your comment" v-model="commentText" @keyup.enter="addComment" />
        <div class="vcomments__add-button" @click="addComment">Add</div>
      </div>
      <comment v-for="(comment, index) in comments" v-bind:key="comment.id" v-bind:comment="comment" v-on:event_child="eventChild"></comment>
    </div> -->
  </v-container>
</template>

<script>
import comment from './comment.vue'

export default {
  components: { comment },
  name: 'CommentPage',

  methods: {
    addComment: function() {
      if (this.commentText.trim() === '') return false;
      var item = {
        id: this.nextId,
        author: this.currentUser,
        text: this.commentText,
        replies: []
      };
      this.comments.push(item);
      this.nextId++;
      this.commentText = '';
    },
    eventChild: function(data) {
      console.log(data, 'data')
      this.lastParent = data.parent_id;
      console.log(data.parent_id, 'check parent_id')
      var item = {
        id: this.nextId,
        author: this.currentUser,
        text: data.text,
        replies: []
      };
      var comment = this.recursiveFind(this.comments, data.parent_id);
      if (comment) {
        comment.replies.push(item);
        this.nextId++;
      }
		},
    recursiveFind: function(replies, id) {
      if (replies) {
        for (var i = 0; i < replies.length; i++) {
          if (replies[i].id === id) {
            return replies[i];
          }
          var found = this.recursiveFind(replies[i].replies, id);
          if (found) return found;
        }
      }
    },
  },

  data: () => ({
    comments: [
      {
        id: 1,
        author: "Alien",
        text: "1",
        replies: [
          {
            id: 2,
            author: "Pete",
            text: "Ill",
            replies: [
              {
                id: 2,
                author: "Pete",
                text: "Ill",
                replies: [
                  {
                    id: 2,
                    author: "Pete",
                    text: "Ill",
                    replies: []
                  },
                ]
              },
              {
                id: 3,
                author: "Pete",
                text: "Ill",
                replies: [
                  {
                    id: 2,
                    author: "Pete",
                    text: "Ill",
                    replies: []
                  },
                ]
              },
            ]
          },
        ]
      },
      {
        id: 8,
        author: "Hermione",
        text: "Rer",
        replies: [
          {
              id: 9,
              author: "Dumbledore",
              text: "Non,",
              replies: []
          },
          {
            id: 10,
            author: "Minerva",
            text: "Acc",
            replies: [
              {
                id: 11,
                author: "Severus",
                text: "Itaque do",
                replies: []
              },
              {
                id: 12,
                author: "Regulus",
                text: "Repellend",
                replies: [
                  {
                    id: 13,
                    author: "Nagini",
                    text: "Exp",
                    replies: []
                  },
                ]
              },
              {
                id: 14,
                author: "Neville",
                text: "Similique nemo, even",
                replies: []
              },
            ]
          },
        ]
      },
    ],
    commentText: '',
    currentUser: 'Harry Potter',
    nextId: 30,
    lastParent: null
  })

}
</script>

<style>

</style>