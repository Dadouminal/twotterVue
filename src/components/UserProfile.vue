<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="title user-profile__username">@{{ user.username }}</h1>
      <div class="tag user-profile__admin-badge" v-if="user.isAdmin">Admin</div>

      <div class="user-profile__follower-count">
        <strong>Followers: {{ followers }}</strong>
      </div>
      <form
        action=""
        class="user-profile__create-twoot"
        @submit.prevent="createTwoot"
        :class="{ exceeded: newTwootCharacterCount > 180 }"
      >
        <label class="label" for="newTwoot"
          ><strong>New Twoot</strong>{{ newTwootCharacterCount }}/180</label
        >
        <textarea
          class="textarea is-link"
          name=""
          id="newTwoot"
          rows="4"
          v-model="newTwootContent"
        ></textarea>
        <div class="user-profile__create-twoot-type">
          <label for="newtwootType"><strong>Type:</strong> </label>
          <select
            class="select"
            name=""
            id="newtwootType"
            v-model="selectedTwootType"
          >
            <option
              :value="option.value"
              v-for="(option, index) in TwootType"
              :key="index"
            >
              {{ option.name }}
            </option>
          </select>
        </div>
        <button class="button is-info">Twoot !</button>
      </form>
    </div>
    <div class="user-profile__twoots-wrapper">
      <TwootItem
        v-for="twoot in user.twoots"
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
        @favorite="toggleFavorite"
      />
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem.vue";

export default {
  name: "UserProfile",
  components: { TwootItem },
  data() {
    return {
      newTwootContent: "",
      selectedTwootType: "instant",
      TwootType: [
        { value: "draft", name: "draft" },
        { value: "instant", name: "Instant twoot" },
      ],
      followers: 0,
      user: {
        id: 1,
        username: "Dadouminal",
        firstName: "Dadou",
        lastName: "Minal",
        email: "jdarius164@gmail.com",
        isAdmin: true,
        twoots: [
          {
            id: 1,
            content: "Super Twoots",
          },
          {
            id: 2,
            content: "Don't forget to subscribe to the eatrh is square",
          },
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
    newTwootCharacterCount() {
      return this.newTwootContent.length;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavorite(id) {
      console.log(`favorite id :#${id}`);
    },
    createTwoot() {
      if (this.newTwootContent && this.selectedTwootType !== "draft") {
        this.user.twoots.unshift({
          id: this.user.twoots.lenght + 1,
          content: this.newTwootContent,
        });
        this.newTwootContent = "";
      }
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style scoped lang="scss">
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;

  .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: #fff;
    border-radius: 5px;
    border: 1px solid #dfe3e8;

    .user-profile__admin-badge {
      background: rgb(116, 12, 212);
      color: white;
      border-radius: 5px;
      margin-right: auto;
      padding: 0 10px;
      font-weight: bold;
      margin-bottom: 20px;
    }
  }
}

h1 {
  margin: 0;
}

.user-profile__create-twoot {
  border-top: 1px solid black;
  display: flex;
  flex-direction: column;

  &.exceeded {
    color: red;
    border-color: crimson;
  }
}
</style>
