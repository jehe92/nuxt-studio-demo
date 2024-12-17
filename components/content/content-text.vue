<template>
  <div
    class="flex w-full flex-col"
    :class="[contentStyleObject]">
    <div
      :class="textStyleObject"
      class="h-full">
      <div class="text-editor">
        <slot></slot>
      </div>
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
    // align text center
    textCenter: {
      type: Boolean,
      required: false,
      default: false,
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
    // Color of text background
    bg: {
      type: String,
      required: false,
      default: "none",
      validator(value) {
        //none, light (light grey), dark (dark blue)
        return ["light", "dark", "none", "white"].includes(value);
      },
    },
    // Size of text
    textSize: {
      type: String,
      required: false,
      default: "normal",
      validator(value) {
        return ["small", "normal", "large"].includes(value);
      },
    },
    // set padding for text when displayed as textbox
    textPadding: {
      type: Boolean,
      default: false,
      required: false,
    },
    // margin of content element
    contentMargin: {
      type: String,
      required: false,
      default: "md",
      validator(value) {
        return ["none", "xs", "sm", "md", "lg", "xl", "xxl"].includes(value);
      },
    },
    // show text in 2 columns
    textCols: {
      type: Number,
      required: false,
      default: 1,
      validator(value) {
        return [1, 2].includes(value);
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
    "bg-white": props.bg === "white",
    "bg-section-light": props.bg === "light",
    "bg-section-dark text-section-text-invert": props.bg === "dark",
    "bg-none": props.bg === "none",
    "p-5 lg:p-8": props.bg !== "none" && props.textPadding,
    "text-center": props.textCenter,
    "lg:columns-2 lg:gap-20": props.textCols === 2,
  }));

  const contentStyleObject = computed(() => ({
    "mb-0": props.contentMargin === "none",
    "mb-2 last:mb-0 lg:mb-2": props.contentMargin === "xs",
    "mb-4 last:mb-0 lg:mb-4": props.contentMargin === "sm",
    "mb-6 last:mb-0 lg:mb-8": props.contentMargin === "md",
    "mb-8 last:mb-0 lg:mb-12": props.contentMargin === "lg",
    "mb-12 last:mb-0 lg:mb-16": props.contentMargin === "xl",
    "mb-16 last:mb-0 lg:mb-20": props.contentMargin === "xxl",
  }));
</script>
