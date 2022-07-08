<template >
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
    <select>
      <option>По Цене Min</option>
      <option>По Цене Max</option>
      <option>По Наименованию</option>
    </select>
  </div>
  <div class="Frame">
    <InputFields @create="addCard" />
    <CardsList :Cards="Cards" @remove="removeCard" />
  </div>
</template>

<script>
import InputFields from "./InputFields.vue";
import CardsList from "./CardsList.vue";
export default {
  name: "MarketBody",
  components: {
    InputFields,
    CardsList,
  },
  data() {
    return {
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
  methods: {
    addCard(cards) {
      this.Cards.push(cards);
    },
    removeCard(card) {
      this.Cards = this.Cards.filter((p) => p.id !== card.id);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
  margin: 0;
}
.Frame {
  display: flex;
  justify-content: flex-start;
  margin: 20px 20px 0 20px;
  height: 100%;
}

.head {
  display: flex;
  justify-content: space-between;
  align-items: center;
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
