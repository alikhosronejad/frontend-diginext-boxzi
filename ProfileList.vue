<template>
  <div>
    <div>
      <button @click="sortAsc">Sort Ascending</button>
      <button @click="sortDesc">Sort Descending</button>
    </div>
    <div v-for="profile in sortedProfiles" :key="profile.id">
      <ProfileCard :profile="profile" @submit-comment="submitComment" />
    </div>
  </div>
</template>

<script>
import ProfileCard from './ProfileCard.vue';

export default {
  components: {
    ProfileCard
  },
  data() {
    return {
      profiles: [
        // Sample profiles with likes and comments
        { id: 1, name: 'Dr. Smith', likes: 10, comments: [] },
        { id: 2, name: 'Dr. Jones', likes: 20, comments: [] },
        // Add more profiles as needed
      ],
      sortKey: 'likes',
      sortOrder: 'asc'
    };
  },
  computed: {
    sortedProfiles() {
      return this.profiles.slice().sort((a, b) => {
        let modifier = this.sortOrder === 'asc' ? 1 : -1;
        if (a[this.sortKey] < b[this.sortKey]) return -1 * modifier;
        if (a[this.sortKey] > b[this.sortKey]) return 1 * modifier;
        return 0;
      });
    }
  },
  methods: {
    sortAsc() {
      this.sortOrder = 'asc';
    },
    sortDesc() {
      this.sortOrder = 'desc';
    },
    submitComment(profileId, comment) {
      const profile = this.profiles.find(p => p.id === profileId);
      if (profile) {
        profile.comments.push(comment);
      }
    }
  }
};
</script>

<style scoped>
/* Add your styles here */
</style>
