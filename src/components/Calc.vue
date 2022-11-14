<template>
  <div class="card alert-primary">
    <div class="card-body text-left">
      <h2 class="card-title text-center">{{ title }}</h2>
      <p class="card-text h5">{{ message }}</p>
      <hr>
      <div>
        <div class="form-group">
          <label>Formula:</label>
          <textarea class="form-control mb-2" id="textarea1"
            v-model="fomula"></textarea>
        </div>
        <div class="text-center">
          <button class="btn btn-primary" v-on:click="click_11()">=</button>
          <button class="btn btn-primary" v-on:click="click_12()">TAX</button>
          <button class="btn btn-primary" v-on:click="click_13()">+</button>
          <button class="btn btn-primary" v-on:click="click_14()">-</button>
          <button class="btn btn-primary" v-on:click="click_15()">×</button>
          <button class="btn btn-primary" v-on:click="click_16()">÷</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calc',
  props: {
    title: String,
  },
  data() {
    return {
      message: 'Enter expression:',
      fomula:'0',
    }
  },
  methods:{
    click_11:function() {
      let arr = this.fomula.trim().split('\n')
      let last = arr.pop()
      let fn = ''
      for(let  n in arr) {
        if (arr[n].trim() != '') {
          fn += 'let ' + arr[n] + ';'
        }
      }
      fn += 'return ' + last + ';'
      let exp = 'function f(){' + fn + '} f();'
      let ans = eval(exp);
      this.message = 'answer: ' + ans
      let re = arr.join(';').trim()
      if (re != '') { re += ';' }
      re += last
      this.$emit('result-event', re, ans)
    },
     click_12 :function () {
         let tax = 'tax'
         document.getElementById('textarea1').value += "tax"
     },
     click_13 :function () {
         let tax = 'plus'
         document.getElementById('textarea1').value += "+"
     },
     click_14 :function () {
         let tax = 'minus'
         document.getElementById('textarea1').value += "-"
     },
     click_15 :function () {
         let tax = 'multiplied'
         document.getElementById('textarea1').value += "*"
     },
     click_16 :function () {
         let tax = 'divided'
         document.getElementById('textarea1').value += "/"
     }
  }

  }

</script>
