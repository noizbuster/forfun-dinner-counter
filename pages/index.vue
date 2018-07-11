<template>
  <v-layout justify-center align-center>
    <v-flex xs12 sm10 md10>
      <div class="text-xs-center">
        <h1 style="font-size: 7em">저녁 식수조사</h1>
        <h1>{{now.toLocaleString('ko-KR')}}</h1>
      </div>
      <v-card>
        <v-card-title>
        </v-card-title>
        <v-card-text class="text-xs-center">
          <h1 style="font-size: 4em">오늘 저녁 식수인원 : {{count}}</h1>
          <h1 class="headline text-xs-center">오후 4시전까지 저녁식수를 추가해주세요</h1>
          <v-btn large class="headline largeButton" v-on:click="inc(-1)"><v-icon x-large>remove</v-icon></v-btn>
          <v-btn large class="headline largeButton" v-on:click="inc(1)"><v-icon x-large>add</v-icon></v-btn>
        </v-card-text>
        <!-- <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" flat nuxt to="/inspire">Continue</v-btn>
        </v-card-actions> -->
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
  export default {
    data () {
      return {
        count: this.get(),
        now: new Date()
      }
    },
    methods: {
      inc (amount) {
        let numb = this.get()
        numb += amount
        this.count = numb
        localStorage.setItem('counter', numb)
      },
      get () {
        try {
          console.log(localStorage.getItem('counter'))
          if (isNaN(localStorage.getItem('counter'))) {
            return 0
          }
          return parseInt(localStorage.getItem('counter'))
        } catch (e) {
          return 0
        }
      },
      reset () {
        this.count = 0
        localStorage.setItem('counter', '0')
      }
    },
    created () {
      setInterval(() => {
        let prev = this.now
        this.now = new Date()
        console.log('tick tock', prev.getDate(), this.now.getDate())
        if (prev.getDate() !== this.now.getDate()) {
          console.log('time change')
          this.reset()
        }
      }, 1000 * 10)
    }
  }
</script>

<style>
.largeButton {
  height: 200px;
  width: 200px;
}
</style>