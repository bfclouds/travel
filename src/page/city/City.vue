<template>
  <div>
    <city-header />
    <city-search :cities="cities"></city-search>
    <city-list :cities="cities" :hotCities="hotCities" :letter="letter"></city-list>
    <city-alphabet :cities="cities" @change="handleLetterChange"></city-alphabet>
  </div>
</template>

<script>
import CityHeader from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/List'
import CityAlphabet from './components/Alphabet'
import axios from 'axios'

export default {
  name: 'City',
  data () {
    return {
      cities: {},
      hotCities: [],
      letter: ''
    }
  },
  components: {
    CityHeader,
    CitySearch,
    CityList,
    CityAlphabet
  },
  methods: {
    getCityInfo () {
      axios.get('/api/city.json?').then(res => {
        res = res.data
        if (res.ret && res.data) {
          this.cities = res.data.cities
          this.hotCities = res.data.hotCities
        }
      }).catch(res => {
        console.log('加载数据失败了')
      })
    },
    handleLetterChange (letter) {
      this.letter = letter
    }
  },
  mounted () {
    this.lastCity = this.city
    this.getCityInfo()
  }
}
</script>

<style lang="stylus" scoped>
</style>
