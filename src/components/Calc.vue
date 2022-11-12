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
          <button class="btn btn-primary"
            v-on:click="click_1()">CALC</button>
            <button class="btn btn-primary"
            v-on:click="click_2()">TAX</button>
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
    click_1:function() {
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
     click_2 :function () {
         let tax = 'tax'
         document.getElementById('textarea1').value += "tax"
     }
  }

  }

</script>
//document.getElementById("textarea4").value = "blue";