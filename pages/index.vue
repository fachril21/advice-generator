<template>
  <div class="bg-gray-800 min-h-screen">
    <div
      class="container mx-auto min-h-screen flex flex-col items-center justify-center text-white"
    >
      <div
        id="card"
        class="rounded-lg flex flex-col gap-4 items-center justify-center bg-gray-700 p-8 relative"
        :style="{ width: '600px' }"
      >
        <div id="data" class="flex flex-col gap-4 items-center justify-center">
          <div id="id">
            <span class="text-green-300 font-medium">
              ADVICE {{ data.slip.id }}
            </span>
          </div>
          <div id="content">
            <p class="text-2xl font-medium text-center">
              "{{ data.slip.advice }}"
            </p>
          </div>
        </div>

        <div id="separator" class="py-4">
          <img src="~/assets/images/pattern-divider-desktop.svg" alt="" />
        </div>
        <div
          id="button"
          class="w-14 h-14 absolute bottom-0 bg-green-300 rounded-full flex items-center justify-center cursor-pointer transition-all ease-in-out duration-300"
          :style="{ bottom: '-1.75rem' }"
          @click="getData"
        >
          <img src="~/assets/images/icon-dice.svg" alt="" />
        </div>
      </div>
    </div>
    <loading :show="isLoading" />
  </div>
</template>

<script>
import Loading from "~/components/Loading.vue";
export default {
  components: { Loading },
  data() {
    return {
      data: {},
      isLoading: false,
    };
  },
  asyncData(context) {
    return context.app.$axios
      .$get("https://api.adviceslip.com/advice")
      .then((res) => {
        return {
          data: res,
        };
      })
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    getData() {
      this.isLoading = true;
      this.$axios
        .$get("https://api.adviceslip.com/advice")
        .then((res) => {
          this.data = res;
          this.isLoading = false;
        })
        .catch((err) => {
          console.log(err);
          this.isLoading = false;
        });
    },
  },
};
</script>

<style scoped>
#button {
  box-shadow: 0 0 0px 0px #6ee7b7;
}
#button:hover {
  box-shadow: 0 0 16px 4px #6ee7b7;
}
</style>
