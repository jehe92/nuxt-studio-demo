<template>
  <div class="flex w-full flex-col">
    <div
      :class="textStyleObject"
      class="h-full">
      <ContentSlot unwrap="p" />
    </div>
  </div>
</template>

<script setup>
  const props = defineProps({
    // Position of text inside flex container
    textPosition: {
      type: String,
      required: false,
      default: "center",
      validator(value) {
        return ["start", "center", "end"].includes(value);
      },
    },
    // Width of text (in cols: 12 = 100% width)
    textWidth: {
      type: [Number, String],
      required: false,
      default: 12,
      validator(value) {
        return [4, 6, 8, 10, 12, "4", "6", "8", "10", "12"].includes(value);
      },
    },
    // show text in 2 columns
    textCols: {
      type: Number,
      required: false,
      default: 1,
      validator(value) {
        return [1, 2, "1", "2"].includes(value);
      },
    },
  });

  const textStyleObject = computed(() => ({
    "w-full lg:w-4/12": props.textWidth === 4 || props.textWidth === "4",
    "w-full lg:w-6/12": props.textWidth === 6 || props.textWidth === "6",
    "w-full lg:w-8/12": props.textWidth === 8 || props.textWidth === "8",
    "w-full lg:w-10/12": props.textWidth === 10 || props.textWidth === "10",
    "w-full": props.textWidth === 12 || props.textWidth === "12",
    "self-start": props.textPosition === "start",
    "self-center": props.textPosition === "center",
    "self-end": props.textPosition === "end",
    "lg:columns-2 lg:gap-20": props.textCols === 2 || props.textCols === "2",
  }));
</script>
