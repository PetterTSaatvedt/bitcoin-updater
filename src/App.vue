<template>
    <bitcoin-header></bitcoin-header>
    <bitcoin-table></bitcoin-table>
</template>

<script>
import BitcoinTable from './components/BitcoinTable.vue'
import BitcoinHeader from './components/BitcoinHeader.vue'

export default {
  name: 'App',
  components: {
    BitcoinHeader,
    BitcoinTable,
  }
}
</script>

<style>
</style>
