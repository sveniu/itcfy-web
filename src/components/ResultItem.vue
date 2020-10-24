<template>
  <div class="result-item">
    This is a result item:
    {{ data }}
  </div>
</template>

<script>
export default {
  name: "ResultItem",
  props: {
    data: Object,
  },
};
</script>
