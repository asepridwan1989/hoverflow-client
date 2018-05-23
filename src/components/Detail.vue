<template>
  <div style="margin: 20px">
    <div class="card">
      <div class="card-body">
        <h1>{{singArt.title}}</h1>
        <h5>Posted at: {{singArt.createdAt | moment("MMMM Do YYYY, h:mm:ss") }}</h5>
        <h5>Last Update at: {{singArt.updatedAt | moment("MMMM Do YYYY, h:mm:ss") }}</h5>
        <h4 style="text-align: justify;">{{singArt.content}}</h4>
      </div>
      <h5>liked : {{singArt.liked}} times</h5>
      <button type="button" class="btn btn-outline-secondary">vote up</button>
      <button type="button" class="btn btn-outline-secondary">vote down</button>
    </div>
    <br>
    <div class="form-group">
      <h3 for="exampleFormControlTextarea1">Reply Question</h3>
      <textarea class="form-control" id="exampleFormControlTextarea1" rows="5" v-model="comment"></textarea>
      <button type="button" class="btn btn-outline-secondary" @click="addComment">submit</button>
    </div>
  </div>  
</template>

<script>
import {mapState} from 'vuex'
export default {
  name: 'Articledetail',
  data: function () {
    return {
      comment: ''
    }
  },
  created () {
    console.log(this.$route.params.id)
    this.$store.dispatch('getOneArticle', this.$route.params.id)
  },
    computed: {
    ...mapState([
      'singArt'
    ])
  },
  methods: {
    addComment () {
      let body = {
        articleId: this.$route.params.id,
        comment: this.comment
      }
      let headers = {
        token : window.localStorage["blog-token"]
      }
      let payload = {
        body,
        headers
      }
      this.$store.dispatch('addComment', payload)
    }
  }

}
</script>

<style>

</style>