<template>
  <div>
    <h2>Добавьте расход</h2>
    <form action="" @submit.prevent="makeObj">
      <p>Название</p>
      <input type="text" v-model="expenseName" />

      <p>Стоимость</p>
      <input type="text" v-model="expensePrice" />

      <p>Тип затрат</p>
      <select name="" id="" v-model="expenseType">
        <option
          v-for="(type, index) in expensesTypes"
          :key="index"
          :value="index"
        >
          {{ type.name }}
        </option>
      </select>

      <p v-if="expenseName || expensePrice || expenseType">
        Последний добавленный элемент: <br />
        - {{ expenseName ? expenseName : 'Не заполнено' }}; <br />
        - {{ expensePrice ? expensePrice : 'Не заполнено' }}; <br />
        - {{ expenseType ? expenseType : 'Не заполнено' }}.
      </p>

      <div class="button-container">
        <button type="submit">Добавить</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "AddInfo",
  props: {
    expensesTypes: Array,
  },
  data() {
    return {
      expenseName: "",
      expensePrice: "",
      expenseType: "",
    };
  },
  methods: {
    makeObj() {
      this.$emit("addObj", {
        name: this.expenseName,
        price: parseInt(this.expensePrice),
        type: this.expenseType,
      });
    },
  },
  created() {
    // console.log(this.expensesTypes);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
