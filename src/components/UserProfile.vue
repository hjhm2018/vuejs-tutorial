<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">@{{ user.username }}</h1>
      <div class="user-profile_admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile_follower-count">
        <strong> Followers: </strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile_posts-wrapper">
      <!-- {{ user.posts[0] }} -->
      <PostItem
        class="user-profile_post"
        v-for="post in user.posts"
        :key="post.id"
        :username="user.username"
        :post="post"
        @favourite="toggleFavourite"
      >
        {{ post.content }}
      </PostItem>
    </div>

    <!-- - {{ fullName }}
    <button @click="followUser">Follow</button> -->
  </div>
</template>

<script>
import PostItem from "./PostItem";
export default {
  name: "UserProfile",
  components: { PostItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "_HenryHerrera",
        firstName: "Henry",
        lastName: "Herrera",
        email: "henry@henry.com",
        isAdmin: true,
        posts: [
          { id: 1, content: "This page is amazing!" },
          { id: 2, content: "Don't forget to subscribe to my page!" },
        ],
      },
    };
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower`);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName} `;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id) {
      console.log(`Favourite Post #${id}`);
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style>
/* button {
  width: 30%;
  margin: 0 auto;
} */

.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile_user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}

.user-profile_admin-badge {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}

h1 {
  margin: 0;
}
</style>
