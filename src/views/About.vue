<template>
  <div class="flex justify-center flex-col items-center">
    <div
      v-if="user"
      class="md:w-4/12 w-11/12 mx-10 mt-4 pb-10 shadow-2xl rounded-lg bg-white"
    >
      <div class="flex justify-center m-4">
        <img :src="user.avatar" alt="Avatar" />
      </div>
      <h3 class="text-lg text-purple-900 uppercase text-center font-bold">
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