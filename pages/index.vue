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
      const _options = {
        method: 'GET',
        url: 'https://db.ygoprodeck.com/api/v7/cardinfo.php?cardset=metal%20raiders&num=5&offset=0'
      }
      const _result = await this.$axios.$request(_options)
      console.log(_result.data)
      this.data = _result.data
    },
    showDetail (e) {
      console.log(e)
      this.$router.push({ name: 'detail-id', params: { id: e.id } })
    }
  }
}
</script>
