<template>
  <h1>Job Details Page</h1>
  <p>Job Id {{ id }}</p>
</template>

<script>
export default {
  name: "JobDetails",
  props: {
    id: String,
  },
};
</script>

<style scoped></style>
