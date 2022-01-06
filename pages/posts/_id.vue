
<template>

  <div class="container">

    <article>

      <h1 class="title">{{post.title}}</h1>
      <p>{{post.content}}</p>

    </article>

    <aside>

      <h3>Related posts</h3>

        <ul>
          <li v-for="related in relatedPosts" :key="related.title"> <!--                          Loops through each related in relatedPosts -> computed  -->
            <!-- <a :href="`/posts/${related.id}`">{{ related.title }}</a>                        Reloads page onclick   -->
              <!-- <nuxt-link :to="`/posts/${related.id}`">{{ related.title }}</nuxt-link>        Doesent reload page onclick -> nuxt-link :to  -->
              <nuxt-link :to="{name: 'posts-id', params: {id: related.id}}">
                {{ related.title }}

              </nuxt-link>
          </li>
        </ul>

    </aside>
  </div>
</template>

<script>
  export default {

    head () {
      return{
        title: this.post.title,
        meta: [
          { name: 'twitter:title', content: 'Nuxt Fundamentals by Vue School'},
          { name: 'twitter:description', content: 'Nuxt + Vue School = 🍕'},
          { name: 'twitter:image', content: 'https://i.imgur.com/UYP2umJ.png'},
          { name: 'twitter:card', content: 'summary_large_image'}
        ]
      }
    },

    data () {

      return{

        id: this.$route.params.id //Define route of id


      }
    },

    computed: {
      post () {
        return this.$store.state.posts.all.find(post => post.id === this.id) // Show post based on route, eg /balut
      },

      relatedPosts (){
        return this.$store.state.posts.all.filter(post => post.id !== this.id) // Shows all post except present post
      }
    }
  }

</script>

<style scoped>
  .container {
    display: flex;
    justify-content: space-between;
    line-height: 1.5;
  }
  article * {
    margin-bottom: 1rem;
  }
  aside {
    min-width: 280px;
    max-width: 280px;
    padding-left: 2rem;
  }
  .title {
    font-size: 2rem;
  }
</style>
