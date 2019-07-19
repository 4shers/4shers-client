<template>
  <div class="d-flex holder">
    <div class="single-file d-flex">
      <div class="content-head">
        <h4>{{filename}}</h4>
      </div>
      <div v-if="contentType === 'Code'" class="prism-code">
        <prism language="javascript">{{ code }}</prism>
        <small>Here's {{contentType}} by : {{author}}</small>
      </div>

      <div v-if="contentType === 'Pic'" class="img-user">
        <img src="https://images.unsplash.com/photo-1470229722913-7c0e2dbbafd3?ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80" alt="">
        <small>Here's {{contentType}} by : {{author}}</small>
      </div>

      <div class="buttons-share d-flex">
        <!-- Twitter -->
        <a class="btn"
          :href="`https://twitter.com/intent/tweet?text=${urldata}`"
          data-size="large"
          data-text="custom share text"
          data-url="https://dev.twitter.com/web/tweet-button"
          data-hashtags="hacktiv8,demo"
          data-via="twitterdev"
          data-related="twitterapi,twitter"
          style="background-color: #1c94e0; color: #fff;">
        Tweet
        </a>
        <!-- Facebook -->
        <div class="fb-share-button"
          data-href="https://developers.facebook.com/docs/plugins/"
          data-layout="button"
          data-size="small">
            <a style="background-color : #4267b2; color: #fff"
            :href='`https://www.facebook.com/sharer/sharer.php?u=${urldata}`'
              class="fb-xfbml-parse-ignore btn">Bagikan
            </a>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import 'prismjs'
import 'prismjs/themes/prism.css'
import Prism from 'vue-prism-component'

export default {
  name : 'item',
  props : ['itemdetails'],
  data : function () {
    return {
      filename : 'Test.js',
      author : 'Irshadi Bagasputro',
      code : `console.log('Hello World')`,
      urldata : `http://data.com`,
      contentType : 'Pic'
    }
  },
  components : {
    Prism
  }
}

</script>
<style>
  .holder {
    width : 100vw;
    justify-content: center;
  }

  .holder .head-content {
    flex-direction: column;
    /* width : 800px; */
  }
  .single-file {
    justify-content: flex-start;
    flex-direction: column;
    width : 80vw;
    margin-top: 5%;
  }

  .prism-code {
    margin-top: 2.5%;
  }

  .buttons-share {
    margin-top: 5%;
    width : 100%;
    justify-content: flex-end;
  }

  .buttons-share .btn {
    margin-right : 2.5%;
  }

  .img-user {
    margin-top: 2.5%;
    flex-direction: column
  }

  .img-user img {
    width : 80vw;
    height: auto
  }
</style>
