<template>
  <div class="post-item" @click="favouritePost(post.id)">
    <div class="user-profile_post">
      <div class="post-item_user">@{{ username }}</div>
      <div class="post-item_content">
        {{ post.content }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PostItem",
  props: {
    username: {
      type: String,
      required: true,
    },
    post: {
      type: Object,
      required: true,
    },
  },
  methods: {
    favouritePost(id) {
      this.$emit("favourite", id);
    },
  },
};
</script>

<style>
/* button {
  width: 30%;
  margin: 0 auto;
} */

.post-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;
}

.post-item:hover {
  transform: scale(1.1, 1.1);
}

.post-item_user {
  font-weight: bold;
}
</style>
