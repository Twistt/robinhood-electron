<template>
  <tr v-if="quote && instrument">
    <td><ticker-link :symbol="instrument.symbol"></ticker-link></td>
    <td v-money="quote.last_trade_price"></td>
    <td v-money="quote.adjusted_previous_close"></td>
    <td v-money="quote.ask_price"></td>
    <td v-money="quote.bid_price"></td>
  </tr>
</template>
<script>
import TickerLink from '@/components/Common/TickerLink';
import state from '@/state';

export default {
  props: ['data'],
  computed: {
    instrument(){
      return state.getters['robinhood/instrument'](this.data.instrument);
    },
    quote(){
      if(!this.instrument){
        return;
      }

      return state.getters['robinhood/quote'](this.instrument.symbol);
    }
  },
  components: {
    'ticker-link': TickerLink
  }
}
</script>
