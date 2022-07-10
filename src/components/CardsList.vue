<template>
  <transition-group name="CardsList" tag="div" class="CardsList">
    <div class="card" v-for="card in Cards" :key="card.id">
      <img
        src="https://s3-alpha-sig.figma.com/img/488b/7f1f/e88ef4c6003a678c0c9d6a1b91606ae9?Expires=1658102400&Signature=Y3SCqmJ7xFluZwmmk706jEx9owdUMFtSj0Fm63yz0wR~gQ3edL2qjkbuYgOsTp0mS0R0C5GNWFAl0~omYtV--jm9jso9bMfiV9eNb47cG~Ue-5MDRdSh5B9GcYn6TE8KgrrYrSQ8htjfw3si1D8LnO2Riyn6KTS8981k1nEj9OF9wE~qEskYzivpIdl0fzs5KufQMb0KwnThB1~qLfeZBGWcQW1SVl-d0e3JvMpMojUHATU2CR4vVK-uUgO-9uFlaeZxMPCCOGVvAg3gmQSsUHooce3cFmhRsoCoJxWd4APLiIkoMn5oQKWDlHYKJsJ94kMxmdvxJekOlxNfbPi3kg__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA"
      />
      <h4>{{ card.title }}</h4>
      <p>
        {{ card.desc }}
      </p>
      <h1>{{ priceMask(card.price) }} руб.</h1>
      <button @click="$emit('remove', card)" class="delBtn"></button>
    </div>
  </transition-group>
</template>

<script>
export default {
  props: {
    Cards: {
      type: Array,
      required: true,
    },
  },
  methods: {
    priceMask(price) {
      return new Intl.NumberFormat('ru-RU').format(price);
    }
  },
  name: "CardsList",
};
</script>

<style>
.CardsList:nth-child(3n) {
  margin-right: 0;
}
.CardsList:nth-child(27n) {
  margin-bottom: 0;
}
.CardsList-move {
  transition: transform 1s;
}

.CardsList {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  overflow-y: auto;
  padding: 20px 0 20px 0;
  margin-bottom: 40px;
}

.card {
  width: 332px;
  height: 423px;
  background: #FFFEFB;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  margin: 0 0 13px 13px;
  position: relative;
}

.card img {
  width: 332px;
  height: 200px;
  left: 380px;
  top: 83px;
  border-radius: 4px 4px 0px 0px;
}

.card p {
  width: 300px;
  height: 80px;
  left: 396px;
  top: 340px;
  margin: 16px;
  font-family: "Source Sans Pro";
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 20px;
  text-align: left;
}

.card h4 {
  height: 25px;
  left: 396px;
  top: 299px;
  margin: 16px;
  font-family: "Source Sans Pro";
  font-style: normal;
  font-weight: 600;
  font-size: 20px;
  line-height: 25px;
}
.card h1 {
  margin: 16px;
  font-family: "Source Sans Pro";
}

.card:hover {
  transform: scale(1.02);

}

.card:hover > .delBtn {
  display: block;
}

.delBtn {
  width: 32px;
  height: 32px;
  background-color: #FF8484;
  background-image: url("~@/assets/delete.svg");
  background-position: center;
  background-repeat: no-repeat;
  position: absolute;
  border-radius: 10px;
  border:none;
  top: -8px;
  right: -8px;
  display: none;
}

.delBtn:hover {
  background-color: #ff5d5d;
  cursor: pointer;
}
</style>
