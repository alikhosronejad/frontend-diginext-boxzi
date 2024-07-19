<template>
  <div class="profile-card">
    <h3>{{ profile.name }}</h3>
    <p>Likes: {{ profile.likes }}</p>
    <div>
      <input v-model="comment" placeholder="Write a comment..." />
      <button @click="submitComment">Submit</button>
    </div>
    <ul>
      <li v-for="(comment, index) in profile.comments" :key="index">{{ comment }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    profile: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      comment: ''
    };
  },
  methods: {
    submitComment() {
      this.$emit('submit-comment', this.profile.id, this.comment);
      this.comment = '';
    }
  }
};
</script>

<style scoped>
.profile-card {
  border: 1px solid #ccc;
  padding: 1em;
  margin-bottom: 1em;
}
</style>
