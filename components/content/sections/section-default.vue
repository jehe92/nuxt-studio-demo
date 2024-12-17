<template>
  <section
    class="py-12 md:py-20"
    :class="sectionStyleObject">
    <div class="container mx-auto">
      <div
        class="text-editor"
        :class="bg === 'dark' ? '[&>p]:text-white' : ''">
        <slot></slot>
      </div>
    </div>
  </section>
</template>

<script setup>
  // *** Props *** //
  const props = defineProps({
    // id of element
    id: {
      type: String,
      required: false,
    },
    // background color of section
    bg: {
      type: String,
      required: false,
      default: "none",
      validator(value) {
        return ["none", "light", "dark"].includes(value);
      },
    },
  });

  const sectionStyleObject = computed(() => ({
    "bg-gray-200": props.bg === "light",
    "bg-primary text-white": props.bg === "dark",
  }));
</script>
