<template>
  <section class="container">
    <div>
      <ArticleList :posts="posts"></ArticleList>
    </div>
  </section>
</template>

<script>
  // 記事一覧コンポーネントを呼び出し
  import ArticleList from '~/components/ArticleList.vue'

  // contentfulの宣言
  import {createClient} from '~/plugins/contentful.js'
  // 設定情報の取得
  const client = createClient()

  export default {
    // 宣言したコンポーネントをindex.vueで使用する為に定義
    components: {
      ArticleList
    },
    // 変数の宣言
    data () {
      return {
        posts: []
      }
    },
    // データの取得(非同期)
    asyncData ({ env }) {
      // contentfulより記事データを取得
      return client.getEntries({
        // 対象のブログID
        'content_type': env.CTF_BLOG_POST_TYPE_ID,
        // 最大取得件数
        'limit': 10,
      }).then(entries => {
        // 取得出来たのでindex.vueに返却
        return {
          posts: entries.items
        }
      }).catch(console.error)
    }
  }
</script>