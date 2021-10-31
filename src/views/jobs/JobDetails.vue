<template>
  <div v-if="job">
    <h1>{{ job.title }}</h1>
    <p>Job Id {{ job.id }}</p>
    <p>Details {{ job.details }}</p>
  </div>

  <div v-else>
    <p>Loading Job Details...</p>
  </div>
</template>

<script>
export default {
  name: "JobDetails",
  props: {
    id: String,
  },
  data() {
    return {
      job: null,
    };
  },
  mounted() {
    fetch(`http://localhost:3000/jobs/${this.id}`)
      .then((res) => res.json())
      .then((data) => (this.job = data))
      .catch((err) => console.log(err.message));
  },
};
</script>

<style scoped></style>
