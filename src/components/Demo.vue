<template>
  <Page :url="url" :pageSize="pageSize"></Page>
</template>

<script>
import Page from './Hello'

export default {
  data () {
    return {
      pageSize: 100,
      url: 'http://newsapi.gugujiankong.com/Handler.ashx?action=getnews&type=top&count=1000'
    }
  },
  components: { Page }
}
</script>

