<template>
  <div>
    <div>
      <transition name="bounce_" mode="out-in">
      </transition>
    </div>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
export default {
  name: "Like",
  props: {
    post_id: Number,
    likes: Array
  },
  computed: mapGetters(["currentUser"]),
  methods: {
    ...mapActions([
      "addLike",
      "deleteLike",
      "addPostLikes",
      "subtractPostLikes"
    ]),
    async like() {
      
    },
    userLiked() {
      
    }
  }
};
</script>

<style scoped></style>
