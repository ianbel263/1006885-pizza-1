<template>
  <li class="cart-list__item">
    <div class="product cart-list__product">
      <img
        :src="pizza.image"
        class="product__img"
        width="56"
        height="56"
        :alt="pizza.name"
      />
      <div class="product__text">
        <h2>{{ pizza.name }}</h2>
        <ul>
          <li>{{ pizza.size.name }}, {{ pizza.dough.cartDescription }}</li>
          <li>Соус: {{ pizza.sauce.name.toLowerCase() }}</li>
          <li>Начинка: {{ ingredients }}</li>
        </ul>
      </div>
    </div>

    <AppItemCounter
      :item="pizza"
      :classNames="'cart-list__counter'"
      :additionalButtonClassName="'counter__button--orange'"
      @onChangeCount="$emit('onChangeCount', $event)"
    />

    <div class="cart-list__price">
      <b>{{ totalPrice }} ₽</b>
    </div>

    <div class="cart-list__button">
      <router-link
        type="button"
        class="cart-list__edit"
        :to="{ name: 'PizzaEdit', params: { slug: pizza.id } }"
      >
        Изменить
      </router-link>
    </div>
  </li>
</template>

<script>
import AppItemCounter from "@/common/components/ItemCounter";

export default {
  name: "AppCartPizzaItem",
  components: { AppItemCounter },
  props: {
    pizza: {
      type: Object,
      required: true,
    },
  },
  computed: {
    ingredients() {
      return this.pizza.ingredients
        .map((el) => el.name.toLowerCase())
        .join(", ");
    },
    totalPrice() {
      return this.pizza.price * this.pizza.quantity;
    },
    quantity() {
      return this.pizza.quantity;
    },
  },
};
</script>
