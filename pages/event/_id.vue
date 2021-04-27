<template>
  <div>
    <h1>{{ event.title }}</h1>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, error, params }) {
    try {
      const { data } = await $axios.get(
        `http://localhost:3004/events/${params.id}`
      )
      return {
        event: data,
      }
    } catch {
      error({ statusCode: 503, message: 'Unable to fetch an event' })
    }
  },
  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: `What you need to know about event #${this.event.title}`,
        },
      ],
    }
  },
}
</script>

<style></style>
