<template>
  <Layout>
    <!-- Page Header-->
    <header
      class="masthead"
      :style="{
        'background-image': `url(${GRIDSOME_API_URL}${general.cover[0].url})`,
      }"
    >
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="site-heading">
              <h1>{{ general.title }}</h1>
              <span class="subheading">{{ general.subtitle }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content-->
    <div class="container px-4 px-lg-5">
      <div class="row gx-4 gx-lg-5 justify-content-center">
        <div class="col-md-10 col-lg-8 col-xl-7">
          <!-- Post preview-->
          <div v-for="(post, index) in $page.posts.edges" :key="`post${index}`">
            <div class="post-preview">
              <g-link :to="`/post/${post.node.id}`">
                <h2 class="post-title">
                  {{ post.node.title }}
                </h2>
                <h3 class="post-subtitle">
                  {{ post.node.desc }}
                </h3>
              </g-link>
              <p class="post-meta">
                Posted by
                <a href="https://strapi.io/">Strapi</a>
                on {{ post.node.created_at }}
              </p>
              <p>
                <span v-for="tag in post.node.tags" :key="tag.id">
                  <g-link :to="`/tag/${tag.id}`">{{ tag.title }}</g-link>
                  &nbsp;&nbsp;
                </span>
              </p>
            </div>
            <hr class="my-4" />
          </div>
          <!-- Pager-->
          <Pager :info="$page.posts.pageInfo" />
        </div>
      </div>
    </div>
  </Layout>
</template>
<page-query>
query ($page: Int){
  posts:allStrapiPost (perPage:5,page:$page) @paginate{
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        id
        title
        content
        desc
        created_at
        tags{
          id
          title
        }
      }
    }
  }
  allStrapiGeneral{
    edges{
      node{
        id
        title
        subtitle
        cover{
          url
        }
      }
    }
  }
}
</page-query>
<script>
import { Pager } from "gridsome";
export default {
  name: "IndexPage",
  metaInfo: {
    title: "Hello, world!",
  },
  components: {
    Pager,
  },
  computed: {
    general() {
      return this.$page.allStrapiGeneral.edges[0].node;
    },
  },
};
</script>

<style>
.home-links a {
  margin-right: 1rem;
}
</style>
