<template
  ><div class="user-profile">
    <div class="user_profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile__follower-count">
        <strong>Followers:</strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile__tweets-wrapper">
    <TweetItem
          v-for="tweet in state.user.tweets"
          :key="tweet.id"
          :username="state.user.username"
          :tweet="tweet"
      />
      </div>
    </div>
  </div>
</template>

<script>
import TweetItem from './TweetItem';

export default {
  name: "UserProfile",
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "_firstuser",
        firstName: "first",
        lastName: "user",
        email: "firstuser@gmail.com",
        isAdmin: true,
        tweets: [
          {
            id: 1,
            content: "Learning Vue",
          },
          {
            id: 2,
            content:
              "idk why there is no auto style syntax and self closeing quotation marks",
          },
        ],
      },
    };
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5 px;
  border: 1px solid #dfe3eb;
}
.user-profile__admin-badge {
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
