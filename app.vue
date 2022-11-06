<template>
  <div class="max-w-2xl mx-auto mt-9">
    <Head>
      <Title>{{ title }}</Title>
      <!-- <Meta name="description" :content="title" /> -->
    </Head>
    <div
      class="p-4 max-w-md bg-white rounded-lg border shadow-md sm:p-8 dark:bg-gray-800 dark:border-gray-700">
      <div class="flex justify-between items-center mb-4">
        <h3
          class="text-xl font-bold leading-none text-gray-900 dark:text-white">
          {{ title }}
        </h3>
      </div>

      <div class="flow-root">
        <ul role="list" class="divide-y divide-gray-200 dark:divide-gray-700">
          <List v-for="winner in winnersList" :key="winner" :winner="winner" />
        </ul>
      </div>
      <InfiniteLoading class="text-white" @infinite="load" />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import InfiniteLoading from "v3-infinite-loading";
import "v3-infinite-loading/lib/style.css";

let winnersList = ref([]);
let page = ref(1);
let title = ref("Metawin  Winners List");
let limit = ref(10);

const load = async ($state) => {
  try {
    const response = await fetch(
      `https://api.dev.platform.metawin.com/sweepstake/winner?skip=${
        limit.value * page.value
      }&&take=${limit.value}`
    );
    const json = await response.json();
    if (json.length < 10) $state.complete();
    else {
      winnersList.value.push(...json);
      $state.loaded();
    }
    page.value++;
  } catch (error) {
    $state.error();
  }
};
</script>
