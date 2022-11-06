<template>
  <li class="py-3 sm:py-4">
    <div class="flex items-center space-x-5">
      <div class="flex-shrink-0">
        <img
          class="w-8 h-8 rounded-full"
          :src="winner.avatarUrl"
          :alt="winner.displayName" />
      </div>
      <div class="flex-1 min-w-0">
        <p class="text-sm font-medium text-gray-900 truncate dark:text-white">
          {{ winner.displayName }}
        </p>
        <p class="text-sm text-gray-500 truncate dark:text-gray-400">
          {{ formatDate(winner.date) }}
        </p>
      </div>
      <div class="flex-1 min-w-0 ml-32">
        <p class="text-sm font-medium text-gray-900 truncate dark:text-white">
          {{ winner.prize.value }}
        </p>
        <p class="text-sm text-gray-500 truncate dark:text-gray-400">
          {{ winner.prize.name }}
        </p>
      </div>
    </div>
  </li>
</template>
<script setup>
defineProps({
  winner: Object,
});

const formatDate = (localDay) => {
  const date = new Date(localDay);
  return date.toString().substring(0, 10);
};
</script>
