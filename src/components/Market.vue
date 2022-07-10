<template >
  <PreloaderScreen/>
  <div class="head">
    <h1>
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
  <transition name="fade">
    <div v-if="show" class="node">
      <p><strong>{{this.massage}}</strong></p>
    </div>
  </transition>
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
    PreloaderScreen,
},
  data() {
    return {
      massage: null,
      show: false,
      selected: "По Умолчанию",
      Cards: [
        {
          id: 1,
          title: "Наименование товара",
          desc:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "100000",
        },
        {
          id: 2,
          title: "Наименование товара 2",
          desc:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10582",
        },
        {
          id: 3,
          title: "Наименование товара 3",
          desc:
            "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "9989",
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
      this.Cards.push(cards)
      this.saveCards()
      this.show = true
      this.showToggle()
      this.massage = "Товар добавлен!"
    },
    removeCard(card) {
      this.Cards = this.Cards.filter((p) => p.id !== card.id);
      this.saveCards();
      this.show = true
      this.showToggle()
      this.massage = "Товар Удален!"
    },
    saveCards() {
      let parsed = JSON.stringify(this.Cards);
      localStorage.setItem('cards', parsed);
    },
    showToggle(){
			setTimeout(() => {
				this.show = false
			}, 2500)
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
.Frame {
  display: flex;
  justify-content: flex-start;
  height: 100%;
  flex-grow: 1;
}

.head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}

.head h1 {
  text-align: left;
  margin: 0 20px;
  font-family: 'Source Sans Pro';
  font-style: normal;
}

.head select {
  margin-right: 40px;
  margin-top: 10px;
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

.node {
font-family: 'Source Sans Pro';
	display: flex;
	flex-direction: column;
	align-items: center;
	position: absolute;
	width: 130px;
	height: 50px;
	z-index: 9999;
  justify-content: center;
  bottom: 30px;
  right: 40px;
  background: #7BAE73;
  border-radius: 10px;
}

.node p {
  color: #FFFFFF;
  text-shadow: 1px 1px 1px #000;
}

.fade-leave-active {
  transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1);
}
.fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}
</style>
