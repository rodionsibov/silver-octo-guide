<template>
  <div class="w-full flex flex-col justify-center items-center">
    <input
      v-model="text"
      class="p-2 border-purple-500 border-2 rounded md:w-1/2 w-11/12 block"
      type="text"
      placeholder="Enter User here"
    />
    <small class="text-purple-200 mt-1">
      {{ names }}
    </small>
  </div>
  <div class="mt-10 p-4 flex flex-col items-center">
    <div
      class="my-2 text-2xl text-purple-100"
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
  setup() {
    const state = reactive({
      users: [],
      urlIdLookup: {},
      text: "",
      filteredUser: computed(() => updateUser()),
      names: computed(() => state.users.map((user) => user.first_name)),
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
