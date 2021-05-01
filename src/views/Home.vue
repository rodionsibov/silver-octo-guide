<template>
  <div class="w-full flex justify-center">
    <input
      v-model="text"
      class="p-2 border-purple-900 border-2 rounded"
      type="text"
      placeholder="Enter User here"
    />
  </div>
  <div class="mt-10 p-4 flex flex-wrap justify-center">
    <div
      class="ml-4 text-2xl text-purple-900"
      v-for="(user, index) in filteredUser"
      :key="index"
    >
      <router-link :to="`/about/${urlIdLookup[user.first_name]}`">
        {{ user.first_name }}
      </router-link>
    </div>
  </div>
</template>

<script>
import { computed, reactive, toRefs } from "vue";

export default {
  name: "Home",
  setup() {
    const state = reactive({
      users: [],
      urlIdLookup: {},
      text: "",
      filteredUser: computed(() => updateUser()),
    });

    function updateUser() {
      if (!state.text) {
        return [];
      }
      return state.users.filter((user) => user.first_name.includes(state.text));
    }

    fetch("https://reqres.in/api/users")
      .then((res) => res.json())
      .then(({ data }) => {
        console.log(data);
        state.users = data;
        state.urlIdLookup = data.reduce(
          (acc, cur, index) => (acc = { ...acc, [cur.first_name]: index + 1 }),
          {}
        );
      });

    return { ...toRefs(state) };
  },
};
</script>
