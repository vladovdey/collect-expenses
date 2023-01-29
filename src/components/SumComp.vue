<template>
  <div>
    <h2>Итоговый результат:</h2>
    <div class="column-container">
      <div
        class="data-column"
        v-for="(expenseType, idx) in expenses"
        :key="idx"
      >
        <p>{{ expenseType.name }}</p>
        <ul>
          <li v-for="(expenseElem, idx) in expenseType.expensesArr" :key="idx">
            Название: {{ expenseElem.name }}; <br />
            Стоимость: {{ expenseElem.price }}.
          </li>
          <hr>
          <p>
            Итого(<i>за категорию</i>):
            {{ expenseType.expensesSum ? expenseType.expensesSum : 0 }}
          </p>
        </ul>
      </div>
    </div>
    <p>Итого: {{ makeSum }}</p>
  </div>
</template>

<script>
export default {
  name: "SumComp",
  props: {
    expenses: Array,
  },
  data() {
    return {
      expensesSum: [], // expensesSum = [sum[0], sum[1]];
    };
  },
  computed: {
    makeSum() {
      return this.expenses.reduce((prev, curr) => {
        let previous = prev.expensesSum ? prev.expensesSum : 0;
        let current = curr.expensesSum ? curr.expensesSum : 0;
        return previous + current;
      });
    },
  },
};
</script>

<style scoped>
.column-container{
  display: flex;
  justify-content: space-between;
}
.data-column {
  background-color: #c0c5c1;
  width: 100%;
  margin: 0 10px;
  border-radius: 4px;
}
</style>