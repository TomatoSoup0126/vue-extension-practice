<template>
  <div @click="gogo" class="cursor-pointer" title="點擊前往商品頁">
    <div class="card">
      <div class="img-block">
        <img :src="`https://www.owlting.com/business/item/c/480_1/${item.item_id}`">
      </div>
      <h2>{{ item.name }}</h2>
      <p class="text-right text-xl">
        <span class="text-lg">
          {{ item.sale_currency }}
        </span>
        {{ item.price }}
      </p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'ItemCard',
  mounted () {
    axios.get(
      `https://www.owlting.com/openmarket/api/getitem3o.beta2.php?action=LIST&index=0&per=${this.range}&sort=4`
    ).then(res => {
      const randomIndex = Math.round(Math.random() * this.range)
      this.item = res.data.list[randomIndex]
    })
  },
  computed: {
  },
  data () {
    return {
      item: {},
      range: 10
    }
  },
  methods: {
    gogo () {
      chrome.tabs.create({
        url: `https://www.owlting.com/market/items/${this.item.item_id}`
      })
    }
  }
}
</script>

<style scoped>
.cursor-pointer {
  cursor: pointer;
}

.img-block {
  overflow: hidden;
  border-radius: 0.375rem 0.375rem;
}
.card {
  padding: 10px 5px;
}

.text-right {
  text-align: right;
}

.text-lg {
  font-size: 1.125rem;
}

.text-xl {
  font-size: 2.5rem;
}
</style>
