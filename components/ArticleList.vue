<template>
  <section>
    <h1>記事一覧</h1>
    <div v-for="post in posts" :key="post.id">
      タイトル：{{ post.fields.title }}
      本文：{{ post.fields.main_content }}
    </div>
  </section>
</template>

<script>
  export default {
    props: ['posts']
  }
</script>