<template>
  <section class="py-20">
    <div class="container mx-auto space-y-8">
      <!-- title -->
      <h2>
        <ContentSlot
          name="title"
          unwrap="p" />
      </h2>
      <!-- description -->
      <div class="text-md">
        <ContentSlot
          name="description"
          unwrap="p" />
      </div>
      <!-- article list -->
      <div class="grid grid-cols-3 gap-4">
        <nuxt-link
          class="col-span-1 bg-gray-200 p-3 text-content-text"
          v-for="article in articles"
          :key="article.id"
          :to="article._path">
          <div class="mb-4 h-[200px] w-full">
            <img
              :src="article.image.src"
              class="h-full w-full object-cover" />
          </div>
          <div class="text-lg font-bold">{{ article.title }}</div>
          <div>{{ article.description }}</div>
        </nuxt-link>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
  import type { Article } from "~/types";

  const props = defineProps({
    count: {
      type: Number,
      default: 3,
    },
  });

  const { data: articles } = await useAsyncData("articles", () =>
    queryContent<Article>("/articles")
      .where({ _extension: "md" })
      .limit(props.count)
      .sort({ date: -1 })
      .find(),
  );
</script>
