<!DOCTYPE html>

<template>
  <div style="margin-top: 20px">
    <h1 style="margin-left: 60px">SmartCalc</h1>

    <hr />

    <div style="margin-left: 50px">
      <button class="btn btn-primary" style="width: 200px; height: 40px; color: #000; background-color: #3ff;"> {{ display }} </button>
    </div>
    
    <div>
      <table style="margin-left: 50px; margin-top: 10px">
        <tr>
          <div class="btn-group" style="width: 200px">
            <button class="btn bstyle" :disabled="!enabled('7')" @click="handler('7')">7</button>
            <button class="btn bstyle" :disabled="!enabled('8')" @click="handler('8')">8</button>
            <button class="btn bstyle" :disabled="!enabled('9')" @click="handler('9')">9</button>
            <button class="btn bstyle" :disabled="!enabled('+')" @click="handler('+')">+</button>
          </div>
        </tr>
        <tr>
          <div class="btn-group" style="width: 200px">
            <button class="btn bstyle" :disabled="!enabled('4')" @click="handler('4')">4</button>
            <button class="btn bstyle" :disabled="!enabled('5')" @click="handler('5')">5</button>
            <button class="btn bstyle" :disabled="!enabled('6')" @click="handler('6')">6</button>
            <button class="btn bstyle" :disabled="!enabled('-')" @click="handler('-')">-</button>
          </div>
        </tr>
        <tr>
          <div class="btn-group" style="width: 200px">
            <button class="btn bstyle" :disabled="!enabled('1')" @click="handler('1')">1</button>
            <button class="btn bstyle" :disabled="!enabled('2')" @click="handler('2')">2</button>
            <button class="btn bstyle" :disabled="!enabled('3')" @click="handler('3')">3</button>
            <button class="btn bstyle" :disabled="!enabled('*')" @click="handler('*')">*</button>
          </div>
        </tr>
        <tr>
          <div class="btn-group" style="width: 200px">
            <button class="btn bstyle" :disabled="!enabled('(')" @click="handler('(')">(</button>
            <button class="btn bstyle" :disabled="!enabled('0')" @click="handler('0')">0</button>
            <button class="btn bstyle" :disabled="!enabled(')')" @click="handler(')')">)</button>
            <button class="btn bstyle" :disabled="!enabled('/')" @click="handler('/')">/</button>
          </div>
        </tr>
        <tr>
          <div class="btn-group" style="width: 200px">
            <button class="btn blstyle" :disabled="!enabled('=')" @click="handler('=')">=</button>
          </div>
        </tr>
      </table>
    </div>

  </div>
</template>


<!--
  BEGIN GENERATED PART
--->

<script>
export default {
  data() {
    return {
      display: "",
      depth: 0,
      state: "BeginExpr",
    };
  },
  methods: {
    enabled(p) {
      return (this.state === "BeginExpr" && this.isDigit(p))
          || (this.state === "HasNum" && this.isDigit(p))
          || (this.state === "HasNum" && this.isOperator(p))
          || (this.state === "HasExpr" && this.isOperator(p))
          || (this.state === "BeginExpr" && p === "(")
          || (this.state === "HasNum" && p === ")" && this.depth > 0)
          || (this.state === "HasExpr" && p === ")" && this.depth > 0)
          || (this.state === "HasNum" && p === "=" && this.depth === 0)
          || (this.state === "HasExpr" && p === "=" && this.depth === 0);
    },
    handler(p) {
      if (this.state === "BeginExpr" && this.isDigit(p)) {
        this.display += p;
        this.state = "HasNum";
      }
      else if (this.state === "HasNum" && this.isDigit(p)) {
        this.display += p;
        this.state = "HasNum";
      }
      else if (this.state === "HasNum" && this.isOperator(p)) {
        this.display += p;
        this.state = "BeginExpr";
      }
      else if (this.state === "HasExpr" && this.isOperator(p)) {
        this.display += p;
        this.state = "BeginExpr";
      }
      else if (this.state === "BeginExpr" && p === "(") {
        this.depth++;
        this.display += "(";
      }
      else if (this.state === "HasNum" && p === ")" && this.depth > 0) {
        this.depth--;
        this.display += ")";
        this.state = "HasExpr";
      }
      else if (this.state === "HasExpr" && p === ")" && this.depth > 0) {
        this.depth--;
        this.display += ")";
      }
      else if (this.state === "HasNum" && p === "=" && this.depth === 0) {
        this.display = "";
        this.state = "BeginExpr";
      }
      else if (this.state === "HasExpr" && p === "=" && this.depth === 0) {
        this.display = "";
        this.state = "BeginExpr";
      }
    },
    isDigit(p) {
      return (p === "0" || p === "1" || p === "2" || p === "3" || p === "4" || p === "5" || p === "6" || p === "7" || p === "8" || p === "9");
    },
    isOperator(p) {
      return (p === "+" || p === "-" || p === "*" || p === "/");
    },
  },
};
</script>

<!--
  END GENERATED PART
--->

<style>
.bstyle {
  width: 25%; 
  border: 10%; 
  border-color: #000;
  color: white;
  background-color: #07f;
}
.blstyle {
  width: 100%; 
  border: 10%; 
  border-color: #000;
  color: white;
  background-color: #07f;
}
</style>

