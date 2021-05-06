<template>
  <Header title="Small Package Loader"/>
  <div class="container">
    <Instructions :title="title"/>
    <FormControl @submit-action="checkVal" :state="state" />
    <ScanResult :result="result" :message="message" :eval="eval"/>
  </div>
</template>

<script>
import Header from './components/Header'
import Instructions from './components/Instructions'
import FormControl from './components/FormControl'
import ScanResult from './components/ScanResult'

export default {
  name: 'App',
  data() {
    return {
      title: this.getMessage('start'),
      result: true,
      message: 'Waiting for user scan',
      tracking: '',
      container: '',
      carrier: '',
      eval: '',
      state: 'enabled'
    }
  },
  components: {
    Header,
    Instructions,
    FormControl,
    ScanResult
  },
  methods: {
    checkVal(val) {
      if((val.scanned).includes("reset")){
        this.reset(val)
      }else{

        switch(val.step){
          case 1:
            //tracking is always numeric, so verify
            var num = Number(val.scanned)
            var check = Number.isInteger(num)
            console.log('is numeric : '+ check)
            this.result = check
            if(!check){
              this.message = this.getMessage('invalid')
            }else{
              this.tracking = val.scanned
              val.step = 2
              this.title = this.getMessage('container')
            }
            break
          case 2:
            //container number always start with NG
            check = (val.scanned).includes("NG")
            this.result = check
            if(!check){
              this.message = this.getMessage('invalid')
            }else{
              val.step = 3
              this.container = val.scanned
              this.title = this.getMessage("carrier")
            }
            break
          case 3:
              //regardless of result, evaluate for good/bad scan
              this.step = 1
              this.state = 'disabled'
              this.carrier = val.scanned
              this.title = this.getMessage('complete')
              this.evaluate(val)
              break
        }
      }
    },
    evaluate(val) {
      
      const final = {
        tracking : this.tracking,
        container : this.container,
        carrier : this.carrier
      }

      //random result simulation
      const r = Math.floor(Math.random() * 100)
      this.eval = (r % 2 ? 'good' : 'bad')
      
      console.log(final)
      setTimeout(() => this.reset(val),1000)
      setTimeout(() => this.eval = '',2000)
    },
    getMessage(i) {
      var messages = {
        start: 'Scan SHIPPING LABEL to begin',
        invalid: 'Invalid Scan',
        container: 'Scan CONTAINER LABEL',
        carrier: 'Scan CARRIER to finish',
        complete: 'Scan COMPLETE - Sending Data..',
        eval_good: 'GOOD',
        eval_bad: 'ERROR'
      }
      
      return messages[i];
    },
    reset(val) {
      val.step = 1
      this.result = true
      this.title = this.getMessage('start')
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
