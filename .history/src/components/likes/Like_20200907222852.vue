<template>
  <div>
    <div>
      <transition name="bounce_" mode="out-in">
      </transition>
      <span class="star">{{ likes.length }}</span>
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
      if (this.currentUser.token) {
        // we find if user already liked
        const foundLiked = this.likes.find(
          like => like.user_id == this.currentUser.id
        );
        if (foundLiked) {
          // remove like if user already liked
          this.deleteLike(foundLiked.id);
          this.subtractPostLikes(foundLiked);
        } else {
          try {
            const result = await this.addLike({
              id: this.post_id,
              user_id: this.currentUser.id
            });
            this.addPostLikes(result);
          } catch (error) {
            alert(error);
          }
        }
      } else {
        this.$swal
          .fire({
            icon: "info",
            title: "Not Allowed!",
            text: "Sorry, you need to register & sign-in"
          })
          .then(() => {
            this.$router.push({ name: "sign-in" });
          });
      }
    },
    userLiked() {
      
    }
  }
};
</script>

<style scoped></style>
