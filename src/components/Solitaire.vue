<template>
  <div class="solitaire">
    <div class="solitaire__board">
      <div class="cards">
        <div class="cards__slot">
          <div class="cards__deck"></div>
          <div class="cards__deck"></div>
          <div class="cards__deck"></div>
          <div class="cards__deck"></div>
          <div class="cards__deck cards__deck-spade"></div>
          <div class="cards__deck cards__deck-heart"></div>
          <div class="cards__deck cards__deck-diamond"></div>
          <div class="cards__deck cards__deck-club"></div>
        </div>
      </div>
      <div class="cards">
        <div class="cards__slot">
          <div v-for="(deck, key) in cardDecks" :key="key" class="cards__deck">
            <div
              v-for="(card, index) in deck"
              :key="card"
              class="cards__deck-card"
              :style="{'top': getTop(index)}"
              >
              <img :src="getCardImg(card)" alt="">
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="solitaire__footer">
      <div class="solitaire__footer-controls">
        <div>
          <span>NEW GAME</span>
        </div>
        <div>
          <span>UNDO</span>
        </div>
        <div>
          <span>HINT</span>
        </div>
      </div>
      <div class="solitaire__footer-timer">
        <div>
          <span>TIME 00:00</span>
        </div>
        <img src="../assets/castle.svg" alt="">
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
interface cardDecks {
  deck1: Array<string>
  deck2: Array<string>
  deck3: Array<string>
  deck4: Array<string>
  deck5: Array<string>
  deck6: Array<string>
  deck7: Array<string>
  deck8: Array<string>
}
export default Vue.extend({
  name: 'Solitaire',
  data () : {
    pokerCards: Array<string>
    cardDecks: cardDecks
    } {
    return {
      'pokerCards': [
        'spade-01',
        'spade-02',
        'spade-03',
        'spade-04',
        'spade-05',
        'spade-06',
        'spade-07',
        'spade-08',
        'spade-09',
        'spade-10',
        'spade-11',
        'spade-12',
        'spade-13',
        'heart-01',
        'heart-02',
        'heart-03',
        'heart-04',
        'heart-05',
        'heart-06',
        'heart-07',
        'heart-08',
        'heart-09',
        'heart-10',
        'heart-11',
        'heart-12',
        'heart-13',
        'diamond-01',
        'diamond-02',
        'diamond-03',
        'diamond-04',
        'diamond-05',
        'diamond-06',
        'diamond-07',
        'diamond-08',
        'diamond-09',
        'diamond-10',
        'diamond-11',
        'diamond-12',
        'diamond-13',
        'club-01',
        'club-02',
        'club-03',
        'club-04',
        'club-05',
        'club-06',
        'club-07',
        'club-08',
        'club-09',
        'club-10',
        'club-11',
        'club-12',
        'club-13'
      ],
      'cardDecks': {
        'deck1': [],
        'deck2': [],
        'deck3': [],
        'deck4': [],
        'deck5': [],
        'deck6': [],
        'deck7': [],
        'deck8': []
      }
    }
  },

  computed: {
    shuffledDeck () :cardDecks {
      return this.cardDecks
    }
  },

  mounted () {
    this.distributeCards()
  },

  methods: {
    distributeCards () {
      let shuffledDeck = this.shuffleDeck()
      while (shuffledDeck.length > 0) {
        Object.keys(this.cardDecks).forEach((deckName:string) => {
          (this.cardDecks as any)[deckName].push(shuffledDeck.pop())
        })
      }
    },

    shuffleDeck ():Array<string> {
      let shuffledDeck = [ ...this.pokerCards ]
      for (let i = this.pokerCards.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1))
        let temp = shuffledDeck[i]
        shuffledDeck[i] = shuffledDeck[j]
        shuffledDeck[j] = temp
      }
      return shuffledDeck
    },

    getCardImg (card:string):string {
      return card ? require(`../assets/${card}.png`) : null
    },

    getTop (idx:number):string {
      return `${idx * 35}px`
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass">
.solitaire
  max-width: 100%
  height: 100%
  background-color:#044444
  display: flex
  flex-direction: column
  padding-left: 3%
  padding-right: 3%
  &__board
    width: 100%
    height: 90%
    padding-top: 1rem
  &__footer
    width: 100%
    height: 10%
    padding-top: 1rem
    padding-bottom: 1rem
    color: #969695
    font-family: Krub, sans-serif
    display: flex
    align-items: flex-end
    justify-content: space-between
    & div
      flex-grow: 1
  &__footer-controls
    font-size: 24px
    display: flex
    justify-content: space-around
    & div
      cursor: pointer
  &__footer-timer
    text-align: right
    border-bottom: solid 1px #fff
    display: flex
    justify-content: space-between
    align-items: flex-end
    & img
      width: 200px
      height: 200px
    & div
      padding: 1rem
      margin: 1rem
      & span
      font-size: 24px
.cards
  width: 100%
  min-height: 184px
  margin-bottom: 1%
  &__slot
    display: grid
    grid-gap: 2%
    grid-auto-flow: column
    height: 184px
  &__deck
    width: 130px
    height: 100%
    position: relative
    background-color: rgba(255, 255, 255, 0.1)
    background-image: url('~@/assets/rec.svg')
    background-position: center
    background-repeat: no-repeat
    background-size: contain
  &__deck-card
    position: absolute
    top: 0
    left: 0
    & img
      width: 100%
      height: 100%
  &__deck-spade
    background-image: url('~@/assets/Spade.svg')
    border: none
    height: 100% !important
  &__deck-heart
    background-image: url('~@/assets/Heart.svg')
    border: none
    height: 100% !important
  &__deck-diamond
    background-image: url('~@/assets/Diamond.svg')
    border: none
    height: 100% !important
  &__deck-club
    background-image: url('~@/assets/Club.svg')
    border: none
    height: 100% !important
</style>
