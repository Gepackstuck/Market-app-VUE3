<template >
<PreloaderScreen/>
  <div class="head">
    <h1
      style="
        text-align: left;
        margin: 0 20px;
        font-family: 'Source Sans Pro';
        font-style: normal;
      "
    >
      Добавление товара
    </h1>
    <select v-model="selected">
      <option value="По Умолчанию" selected="selected">По Умолчанию</option>
      <option value="title">По Наименованию</option>
      <option value="min">По Цене Min</option>
      <option value="max">По Цене Max</option>
    </select>
  </div>
  <div class="Frame">
    <InputFields @create="addCard" />
    <CardsList :Cards="sortedList" @remove="removeCard" />
  </div>
</template>

<script>
import InputFields from "./InputFields.vue";
import CardsList from "./CardsList.vue";
import PreloaderScreen from "./PreloaderScreen.vue";
export default {
  name: "MarketBody",
  components: {
    InputFields,
    CardsList,
    PreloaderScreen
},
  data() {
    return {
      selected: "По Умолчанию",
      Cards: [
        {
          id: 1,
          title: "Наименование товара",
          desc:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 000",
        },
        {
          id: 2,
          title: "Наименование товара 2",
          desc:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 582",
        },
        {
          id: 3,
          title: "Наименование товара 3",
          desc:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 313",
        },
      ],
    };
  },
  computed:{
    sortedList () {
        switch(this.selected){
            case 'title': return this.Cards.slice().sort(sortByTitle);
            case 'min': return this.Cards.slice().sort(sortByMinPrice);
            case 'max': return this.Cards.slice().sort(sortByMaxPrice);
            default: return this.Cards;
        }
    }
  },
  mounted() {
    if(localStorage.getItem('cards')) {
      try {
        this.Cards = JSON.parse(localStorage.getItem('cards'));
      } catch(e) {
        localStorage.removeItem('cards');
      }
    }
  },
  methods: {
    addCard(cards) {
      this.Cards.push(cards);
      this.saveCards();
    },
    removeCard(card) {
      this.Cards = this.Cards.filter((p) => p.id !== card.id);
      this.saveCards();
    },
    saveCards() {
      let parsed = JSON.stringify(this.Cards);
      localStorage.setItem('cards', parsed);
    }
  },
};
  const sortByTitle = (card1, card2) => card1.title.toLowerCase() > card2.title.toLowerCase() ? 1 : -1;
  const sortByMinPrice = (card1, card2) => +card1.price > +card2.price ? 1 : -1;
  const sortByMaxPrice = (card1, card2) => +card1.price < +card2.price ? 1 : -1;
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("//fonts.googleapis.com/css?family=Source+Sans+Pro:300,400,700,400italic");
body {
  margin: 0;
}
.Frame {
  display: flex;
  justify-content: flex-start;
  padding: 20px 20px 0 20px;
  height: 100%;
  flex-grow: 1;
  
  background: rgba(235, 235, 235, 0.8);
}

.head {
  display: flex;
  justify-content: space-between;
  align-items: center;
    background: rgba(235, 235, 235, 0.8);
}

.head select {
  margin-right: 40px;
  margin-top: 20px;
  width: 120;
  height: 36px;
  left: 1287px;
  top: 31px;
  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  font-family: "Source Sans Pro";
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  color: #B4B4B4;
  border: none;
}

.head select:focus {
  transform: scale(1.02);
  outline: none;
}
</style>
