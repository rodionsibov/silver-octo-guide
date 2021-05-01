<template>
  <div class="flex justify-center">
    <div
      v-if="user"
      class="md:w-4/12 w-11/12 mx-10 mt-4 pb-10 shadow-2xl rounded-lg bg-purple-50"
    >
      <div class="flex justify-center m-4">
        <img class="rounded-full" :src="user.avatar" alt="Avatar" />
      </div>
      <h3 class="text-2xl text-yellow-400 uppercase text-center font-extrabold">
        {{ user.first_name }}
        {{ user.last_name }}
      </h3>
      <h5 class="text-gray-700 text-center">
        {{ user.email }}
      </h5>
    </div>
  </div>
</template>

<script>
import { useRoute } from "vue-router";
import { reactive, toRefs } from "vue";

export default {
  setup() {
    const route = useRoute();
    const state = reactive({
      user: null,
    });

    fetch(`https://reqres.in/api/users/${route.params.slug}`)
      .then((res) => res.json())
      .then(({ data }) => {
        console.log(data);
        state.user = data;
      });

    return { ...toRefs(state) };
  },
};
</script>