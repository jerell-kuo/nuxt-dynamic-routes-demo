<template>
  <v-container grid-list-md>
    <v-data-table
      :headers="headers"
      :items="data"
      :items-per-page="5"
      class="elevation-1"
      @click:row="showDetail"
    />
  </v-container>
</template>

<script>
export default {
  name: 'IndexPage',
  data () {
    return {
      data: [],
      headers: [
        { text: 'name', value: 'name' },
        { text: 'race', value: 'race' },
        { text: 'type', value: 'type' },
        { text: 'atk', value: 'atk' },
        { text: 'attribute', value: 'attribute' }
      ]
    }
  },
  mounted () {
    this.fetchAPI()
  },
  methods: {
    async fetchAPI () {
      /* axios GET method 寫法之一 */
      const _options = {
        method: 'GET',
        url: 'https://db.ygoprodeck.com/api/v7/cardinfo.php?cardset=metal%20raiders&num=5&offset=0'
      }
      const _result = await this.$axios.$request(_options)
      console.log(_result.data)
      this.data = _result.data

      /* axios GET method 寫法之二 */
      // const _url = 'https://db.ygoprodeck.com/api/v7/cardinfo.php?cardset=metal%20raiders&num=5&offset=0'
      // const _result = await this.$axios.$get(_url)

      /* axios POST method 寫法之一 */
      // const _options = {
      //   method: 'POST',
      //   url: 'https://db.ygoprodeck.com/api/v7/cardinfo.php?cardset=metal%20raiders&num=5&offset=0',
      //   headers : {
      //    xxxxxxx: xxxxxxxxxx
      //   }
      // }
      // const _result = await this.$axios.$request(_options)

      /* axios POST method 寫法之二 */
      // const _url = 'https://db.ygoprodeck.com/api/v7/cardinfo.php?cardset=metal%20raiders&num=5&offset=0'
      // const _pkg = { xxxx: xxxx }
      // const _config = { headers: xxxxxxxxxxxxx }
      // const _result = await this.$axios.$get(_url , _pkg, config)
    },
    showDetail (e) {
      console.log(e)
      this.$router.push({ name: 'detail-id', params: { id: e.id } })
    }
  }
}
</script>
