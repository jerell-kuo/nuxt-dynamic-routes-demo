<template>
  <v-container fluid>
    <v-layout column>
      <v-card>
        <v-card-text>
          <v-flex class="mb-4">
            <v-avatar size="96" class="mr-4">
              <img :src="image" alt="Avatar">
            </v-avatar>
          </v-flex>
          <v-text-field
            v-model="name"
            label="name"
          />
        </v-card-text>
      </v-card>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  name: 'CardDetail',
  data () {
    return {
      cardData: null,
      image: '',
      name: ''
    }
  },
  async fetch () {
    await this.getCardDetail()
  },
  methods: {
    async getCardDetail () {
      const _options = {
        method: 'GET',
        url: `https://db.ygoprodeck.com/api/v7/cardinfo.php?id=${this.$route.params.id}`
      }
      const _result = await this.$axios.$request(_options)
      console.log(_result.data)
      this.cardData = _result.data[0]
      this.image = this.cardData.card_images[0].image_url
      this.name = this.cardData.name
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
