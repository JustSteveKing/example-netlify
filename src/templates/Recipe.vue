<template>
  <Layout>
    <div class="post-title">
      <h1 class="post-title__text">
        {{ $page.recipe.title }}
      </h1>

      <PostMeta :post="$page.recipe" />

    </div>

    <div class="post content-box">
      <div class="post__header">
        <g-image alt="Cover image" v-if="$page.recipe.cover_image" :src="$page.recipe.cover_image" />
      </div>

      <div class="post__content" v-html="$page.recipe.content" />

    </div>

    <div class="post-comments">
      <!-- Add comment widgets here -->
    </div>

    <Author class="post-author" />
  </Layout>
</template>

<script>
import PostMeta from '~/components/PostMeta'
import Author from '~/components/Author.vue'

export default {
  components: {
    Author,
    PostMeta,
  },
  metaInfo () {
    return {
      title: this.$page.recipe.title,
      meta: [
        {
          name: 'description',
          content: this.$page.recipe.description
        }
      ]
    }
  }
}
</script>

<page-query>
query Recipe ($id: ID!) {
  recipe: recipe (id: $id) {
    title
    path
    date (format: "D. MMMM YYYY")
    timeToRead
    description
    prep_time
    cook_time
    ingredients
    instructions
    cover_image (width: 860, blur: 10)
  }
}
</page-query>

<style lang="scss">
.post-title {
  padding: calc(var(--space) / 2) 0 calc(var(--space) / 2);
  text-align: center;
}

.post {

  &__header {
    width: calc(100% + var(--space) * 2);
    margin-left: calc(var(--space) * -1);
    margin-top: calc(var(--space) * -1);
    margin-bottom: calc(var(--space) / 2);
    overflow: hidden;
    border-radius: var(--radius) var(--radius) 0 0;

    img {
      width: 100%;
    }

    &:empty {
      display: none;
    }
  }

  &__content {
    h2:first-child {
      margin-top: 0;
    }

    p:first-of-type {
      font-size: 1.2em;
      color: var(--title-color);
    }

    img {
      width: calc(100% + var(--space) * 2);
      margin-left: calc(var(--space) * -1);
      display: block;
      max-width: none;
    }
  }
}

.post-comments {
  padding: calc(var(--space) / 2);

  &:empty {
    display: none;
  }
}

.post-author {
  margin-top: calc(var(--space) / 2);
}
</style>
