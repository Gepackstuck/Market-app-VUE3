<template>
  <div class="InputFields">
    <p>Наименование товара</p>
    <input
      v-bind:value="cards.title"
      @input="cards.title = $event.target.value"
      class="leftInput"
      placeholder="Введите наименование товара"
      required
    />
    <p>Описание товара</p>
    <input
      v-bind:value="cards.desc"
      @input="cards.desc = $event.target.value"
      class="discript"
      placeholder="Введите описание товара"
      required
    />
    <p>Ссылка на изображение товара</p>
    <input
      class="leftInput"
      placeholder="Введите ссылку"
      value="https://s3-alpha-sig.figma.com/img/488b/7f1f/e88ef4c6003a678c0c9d6a1b91606ae9?Expires=1658102400&Signature=Y3SCqmJ7xFluZwmmk706jEx9owdUMFtSj0Fm63yz0wR~gQ3edL2qjkbuYgOsTp0mS0R0C5GNWFAl0~omYtV--jm9jso9bMfiV9eNb47cG~Ue-5MDRdSh5B9GcYn6TE8KgrrYrSQ8htjfw3si1D8LnO2Riyn6KTS8981k1nEj9OF9wE~qEskYzivpIdl0fzs5KufQMb0KwnThB1~qLfeZBGWcQW1SVl-d0e3JvMpMojUHATU2CR4vVK-uUgO-9uFlaeZxMPCCOGVvAg3gmQSsUHooce3cFmhRsoCoJxWd4APLiIkoMn5oQKWDlHYKJsJ94kMxmdvxJekOlxNfbPi3kg__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA"
      style="opacity: 50%"
      readonly
    />
    <p>Цена товара</p>
    <input
      v-bind:value="cards.price"
      @input="cards.price = $event.target.value"
      class="leftInput"
      placeholder="Введите цену"
      required
    />
    <button class="addbtn" @click="addCard">Добавить товар</button>
  </div>
</template>

<script>
export default {
  name: "InputFields",
  data() {
    return {
      cards: {
        title: "",
        desc: "",
        price: "",
      },
    };
  },
  methods: {
    addCard() {
      if (this.title !== "" || this.desc !== "" || this.price !== "") {
        this.cards.id = Date.now();
        this.$emit("create", this.cards);
        this.cards = {
          title: "",
          desc: "",
          price: "",
        };
      }
    },
  },
};
</script>

<style>
.InputFields {
  display: flex;
  flex-direction: column;
  width: 332px;
  height: 420px;
  left: 32px;
  top: 83px;
  border: none;
  background: #FFFEFB;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  padding-top: 16px;
}

.InputFields p {
  text-align: left;
  margin: 0 20px;
  font-family: "Source Sans Pro";
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 13px;
  letter-spacing: -0.02em;
  color: #49485E;
  cursor: default;
}

.addbtn {
  width: 284px;
  height: 36px;
  left: 56px;
  top: 463px;
  background: #EEEEEE;
  border-radius: 10px;
  margin: 20px;
  border: none;
  margin-top: 0px;
  font-family: "Inter";
  font-style: normal;
  font-weight: 600;
  font-size: 12px;
  line-height: 15px;
  text-align: center;
  letter-spacing: -0.02em;
  color: #B4B4B4;
}

.addbtn:hover {
  cursor: not-allowed;
}

.discript {
  width: 274px;
  height: 100px;
  left: 56px;
  top: 193px;
  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  margin: 4px 20px 20px 20px;
  border: none;
  font-family: "Source Sans Pro";
  padding-left: 10px;
  vertical-align: top;
}

.discript:focus {
  transform: scale(1.02);
  outline: none;
}

.leftInput {
  width: 274px;
  height: 36px;
  left: 56px;
  top: 124px;
  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  margin: 4px 20px 20px 20px;
  border: none;
  font-family: "Source Sans Pro";
  padding-left: 10px;
}

.leftInput:focus {
  transform: scale(1.02);
  outline: none;
}
</style>
