<template>
  <div>
    <h1>Cart</h1>
    <table>
      <thead>
        <tr>
          <th class="robot-title">
            Robot
          </th>
          <th class="cost">
            Cost
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(robot, index) in cart" :key="index">
          <td class="robot-title">
            {{robot.head.title}}
          </td>
          <td class="cost">
            {{robot.cost}}
          </td>
        </tr>
      </tbody>
    </table>
    <h2 class="saleItems">You saved money on these robots:</h2>
    <table>
      <thead>
        <tr>
          <th class="robot-title">
            Robot
          </th>
          <th class="cost">
            Cost
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(robot, index) in cartSaleOnly" :key="index">
          <td class="robot-title">
            {{robot.head.title}}
          </td>
          <td class="cost">
            {{robot.cost}}
          </td>
        </tr>
      </tbody>
    </table>
 </div>
</template>

<script lang="ts">
import {
  defineComponent, Ref, computed,
} from 'vue';
import Cart from '@/data/Cart';
import { useStore } from 'vuex';

export default defineComponent({
  name: 'ShoppingCart',
  setup() {
    const store = useStore();
    const cart: Ref<Cart[]> = computed(() => store.state.cart);
    const cartSaleOnly: Ref<Cart[]> = computed(() => store.getters.cartSaleItems);

    return {
      cart,
      cartSaleOnly,
    };
  },
});
</script>

<style scoped>
  td, th {
    padding: 5px;
  }
  .robot-title {
    text-align: left;
    padding-right: 200px;
  }
  .cost {
    text-align: right;
  }
  .saleItems {
    margin-top: 50px;
    font-size: 18px;
    color: red;
  }
</style>
