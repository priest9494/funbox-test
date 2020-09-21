<template>
  <div class="app">
    <div class="background">
      <div class="title">
        Ты сегодня покормил кота?
      </div>

      <div class="card-wrapper">
        <Food-card
          class="food-card"
          v-bind:tasteLine="'фуа-гра'"
          v-bind:portionsCount="'10'"
          v-bind:mouseCount="'1'"
          v-bind:weight="'0,5'"
          v-bind:clientLine="''"
          v-bind:enabled="true"
          v-bind:selectedText="'Печень утки разварная с артишоками.'"
        ></Food-card>

        <Food-card 
          class="food-card"
          v-bind:tasteLine="'рыбой'"
          v-bind:portionsCount="'40'"
          v-bind:mouseCount="'2'"
          v-bind:weight="'2'"
          v-bind:clientLine="''"
          v-bind:enabled="true"
          v-bind:selectedText="'Головы щучьи с чесноком да свежайшая сёмгушка.'"
        ></Food-card>

        <Food-card 
          class="food-card"
          v-bind:tasteLine="'курой'"
          v-bind:portionsCount="'100'"
          v-bind:mouseCount="'5'"
          v-bind:weight="'5'"
          v-bind:clientLine="'заказчик доволен'"
          v-bind:enabled="false"
          v-bind:selectedText="'Филе из цыплят с трюфелями в бульоне.'"
        ></Food-card>
      </div>
      
    </div>
  </div>
</template>

<script>
import FoodCard from './components/FoodCard.vue'

export default {
  name: 'App',
  components: {
    FoodCard
  }
}
</script>

<style lang="scss">
  body {
    margin: 0;
    padding: 0;

    .app {
      .background {
        background: url(./assets/background.png);
        background-position: center center;
        background-size: cover;
        min-height: 100vh;
        min-width: 100vw;
        box-shadow: inset 0 25vh 30px  -15px rgba(0, 0, 0, 0.2), inset 0 -25vh 30px  -15px rgba(0, 0, 0, 0.2);

        .title {
          padding-top: 40px;
          font-family: 'Exo 2.0', sans-serif;
          text-align: center;
          font-size: 36px;
          color: #fff;
        }

        .card-wrapper {
          display: flex;
          flex-wrap: wrap;
          justify-content: space-around;

          .food-card {
            margin-top: 30px;
          }
        }
      }
    }
  }
</style>