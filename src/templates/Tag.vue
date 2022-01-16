<template>
  <Layout>
    <!-- Page Header-->
    <header class="masthead" style="background-image: url('/img/post-bg.jpg')">
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="site-heading">
              <h1># {{ $page.tag.title }}</h1>
              <span class="subheading"
                >Created At {{ $page.tag.created_at }}</span
              >
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
          <div v-for="(post, index) in $page.tag.posts" :key="`post${index}`">
            <div class="post-preview">
              <g-link :to="`/post/${post.id}`">
                <h2 class="post-title">
                  {{ post.title }}
                </h2>
              </g-link>
            </div>
            <hr class="my-4" />
          </div>
        </div>
      </div>
    </div>
  </Layout>
</template>
<page-query>
query ($id: ID!){
  tag:strapiTag(id:$id){
    title
    created_at
    posts{
      id
      title
      desc
      created_at
    }
  }
}
</page-query>
<script>
export default {
  name: "TagPage",
};
</script>
