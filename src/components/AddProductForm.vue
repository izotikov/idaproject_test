<template>
  <form class="inputForm" v-on:submit.prevent>
    <div class="inputForm__nameAndAreaFlex" style="margin-top: 16px">
      <div class="inputForm__positionOfRedDot"> <!-- Наименование товара -->
        <span class="inputForm__name">Наименование товара</span>
        <img
            class="redDot"
            v-bind:src="require('../img/Rectangle.svg')"
            alt="red_dot"
        >
      </div>
      <input
          class="inputForm__textarea"
          type="text"
          placeholder="Введите наименование товара"
          v-model="product.name"
          @focus="focusedName=true"
          :class="{invalidForm: focusedName && !checkName()}"
      >
      <div v-if="focusedName && !checkName()" class="invalidForm__inscription">{{errorName}}</div>
    </div>
    <div class="inputForm__nameAndAreaFlex">
      <span class="inputForm__name">Описание товара</span> <!-- Описание товара -->
      <textarea
          class="inputForm__textarea"
          rows="7"
          placeholder="Введите описание товара"
          v-model="product.description"
      />
    </div>
    <div class="inputForm__nameAndAreaFlex">
      <div class="inputForm__positionOfRedDot">
        <span class="inputForm__name">Ссылка на изображение товара</span>
        <img
            class="redDot"
            v-bind:src="require('../img/Rectangle.svg')"
            alt="red_dot"
        >
      </div> <!-- Ссылка -->
      <input
          class="inputForm__textarea"
          type="text"
          placeholder="Введите ссылку"
          v-model="product.link"
          @focus="focusedLink=true"
          :class="{invalidForm: focusedLink && !checkLink()}"
      >
      <div class="invalidForm__inscription"  v-if="focusedLink && !checkLink()">{{errorLink}}</div>
    </div>
    <div class="inputForm__nameAndAreaFlex">
      <div class="inputForm__positionOfRedDot">
        <span class="inputForm__name">Цена товара</span>
        <img
            class="redDot"
            v-bind:src="require('../img/Rectangle.svg')"
            alt="red_dot"
        >
      </div> <!-- Цена товара -->
      <input
          class="inputForm__textarea"
          type="text"
          placeholder="Введите цену"
          v-model="product.price"
          @change="decoratePrice()"
          @focus="focusedPrice=true"
          :class="{invalidForm: focusedPrice && !checkPrice()}"
      >
      <div  class="invalidForm__inscription"  v-if="focusedPrice && !checkPrice()">{{errorPrice}}</div>
    </div>
    <button
        class="inputForm__button"
        :class="{inputForm__button__valid: checkName() && checkLink() && checkPrice()}"
        @click="createPost()"
        :disabled="!checkName() || !checkLink() || !checkPrice()"
    >
      Добавить товар
    </button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      errorName: "",
      errorLink: "",
      errorPrice: "",
      focusedName: false,
      focusedLink: false,
      focusedPrice: false,
      product: {
        name: "",
        description: "",
        link: "",
        price: "",
        id: 0
      }
    }
  },
  methods: {
    decoratePrice() { // Меняет значение числа на более читаемое после убирания фокусa с инпута
      this.product.price = this.product.price.replace(/(\d)(?=(\d{3})+$)/g, '$1 ');
    },
    checkName() {
      if (this.product.name) {
        return true;
      } else {
        this.errorName = "Поле является обязательным";
        return false;
      }
    },
    checkLink() {
      if (this.product.link) {
        return true;
      } else {
        this.errorLink = "Поле является обязательным";
        return false;
      }
    },
    checkPrice() {
      if (this.product.price) {
        return true;
      } else {
        this.errorPrice = "Поле является обязательным";
        return false;
      }
    },
    createPost() {
      this.product.id = Date.now();
      this.$emit("create", this.product);
      this.product = {
        name: "",
        description: "",
        link: "",
        price: "",
      }
    }
  }
}
</script>

<style scoped lang="scss">
  .inputForm {
    background-color: #FFFEFB;
    font-family: 'Source Sans Pro', sans-serif;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    width: 332px;
    margin-left: 32px;
    display: flex;
    flex-direction: column;
    position: sticky;
    top: 24px;
  }
  .inputForm__name {
    font-size: 10px;
    color: #49485E;
    padding: 0 0 4px 0;
    letter-spacing: -0.02em;
    font-weight: 400;
  }
  .inputForm__textarea {
    font-size: 12px;
    font-weight: 400;
    resize: none;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    outline: none;
    border: none;
    padding: 10px 16px;
    border-radius: 4px;
  }
  .inputForm__textarea::placeholder {
    font-family: 'Source Sans Pro', sans-serif;
    font-weight: 300;
    color: #B4B4B4;
  }
  .inputForm__nameAndAreaFlex {
    display: flex;
    flex-direction: column;
    padding: 8px 24px;
  }
  .inputForm__button {
    padding: 10px;
    text-align: center;
    outline: none;
    border: none;
    letter-spacing: -0.02em;
    color: #B4B4B4;
    width: 85%;
    background-color: #EEEEEE;
    border-radius: 10px;
    align-self: center;
    font-size: 12px;
    margin: 24px 0;
  }
  .redDot {
    width: 4px;
    height: 4px;
  }
  .inputForm__positionOfRedDot {
    display: flex;
  }
  .invalidForm {
    border: 1px solid #FF8484;
  }
  .inputForm__button__valid {
    background-color: #7BAE73;
    color: #FFFFFF;
  }
  .inputForm__button__valid:hover {
    cursor: pointer;
    background-color: #609757;
  }
  .invalidForm__inscription {
    font-size: 8px;
    color: #FF8484;
    margin-top: 4px;
  }
</style>