<template>
  <div class="container">
    <AddInfo @add-obj="addExpense" :expenses-types="expensesTypes" />
    <hr />
    <SumComp :expenses="expenses" />
  </div>
</template>

<script>
import AddInfo from "./components/AddInfo.vue";
import SumComp from "./components/SumComp.vue";

export default {
  name: "App",
  components: {
    AddInfo,
    SumComp,
  },
  data() {
    return {
      expensesTypes: [
        { id: 0, name: "Обязательные расходы" },
        { id: 1, name: "Необязательные расходы" },
      ],
      expenses: [],
    };
  },
  methods: {
    addExpense(obj) {
      if (this.expenses[obj.type].expensesArr) {
        this.expenses[obj.type].expensesArr.push(obj);
        this.expenses[obj.type].expensesSum += obj.price;
      } else {
        this.expenses[obj.type] = Object.assign(this.expenses[obj.type], {
          expensesArr: [obj],
          expensesSum: obj.price,
        });
      }
    },
  },
  watch: {},
  created() {
    /*
    expenses = [
      { id: 0, name: "bla-bla", expensesArray: [obj], expensesSum: 123 },
    ]
    */
    this.expenses = Object.assign(this.expensesTypes);
  },
};
</script>

<style>
body{
  margin: 0;
}
button{
  border: none;
  background-color: rgb(68, 56, 80);
  color: #fff;
  padding: 10px 20px;
  font-size: 18px;
  border-radius: 5px;
  cursor: pointer;
}
button:hover{
  background-color: rgba(68, 56, 80, .9);
}
ul{
  list-style-type: none;
  padding: 0;
}
li{
  margin: 5px 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #c0c5c1;
  padding: 10px;
}
.container{
  max-width: 860px;
  width: 100%;
  margin: 0 auto;
  padding: 10px 15px;
  background-color: #eaf0ce;
  border-radius: 10px;
  text-align: center;
}
.button-container{
  margin-top: 20px;
}
input{
  border: 1px solid #443850;
  border-radius: 4px;
  padding: 5px 10px;
  background-color: #c0c5c1;
}
</style>
