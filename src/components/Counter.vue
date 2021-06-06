<template>
  <div v-if="loaded" class="m-20 border shadow-xl p-5 hover:shadow-2xl  ">
      <section class="lg:text-center  font-mono text-2xl font-semibold text-right">
          <p>Countdown For My Sucess Day 👏 🐱‍💻 Yet to Come...!</p>
      </section>
      <section class="font-mono lg:m-3 lg:justify-center lg:shadow-none counter flex flex-row rounded m-5 content-center">
          <div class="days text-2xl relative lg:text-5xl">
              {{displayDays}}
              <div class="lg:text-sm text-xs absolute">
                  Days
              </div>
              <span class="leading-snug">:</span>
          </div>
          <div class="hours text-2xl lg:text-5xl relative">
              {{displayHours}}
              <div class="lg:text-sm text-xs absolute">
                  Hours
              </div>
              <span class="leading-snug">:</span>
          </div>
          <div class="minutes relative text-2xl lg:text-5xl">
              {{displayMinutes}}
              <div class="lg:text-sm text-xs absolute">
                  Minutes
              </div>
              <span class="leading-snug">:</span>
          </div>
          <div class="seconds text-2xl relative my-auto lg:text-5xl">
              {{displaySeconds}}
              <div class="lg:text-sm text-xs absolute lg:mt-2">
                  Seconds
              </div>
          </div>
      </section>
      <p class="animate-bounce text-3xl lg:text-5xl p-2">🐱‍💻</p>
  </div>
</template>

<script>
export default {
    name:"Counter",
    data(){
        return{
            displayDays:0,
            displayHours:0,
            displayMinutes:0,
            displaySeconds:0,
            loaded: false
        }
    },
    computed:{
        seconds: ()=> 1000,
        minutes(){
            return this.seconds * 60;
        },
        hours(){
            return this.minutes *60;
        },
        days(){
            return this.hours * 24;
        }
    },
    mounted(){
        this.showTime()
    },
    methods:{
        format: num =>(num<10?"0"+num:num),
        showTime(){
            const timer = setInterval(()=>{
                const now = new Date();
                const end = new Date(2022,1,1,10,10,10);
                const distance = end.getTime() - now.getTime();

                if(distance < 0){
                    clearInterval(timer);
                    return;
                }

                const _days = Math.floor(distance/this.days);
                const _hours = Math.floor((distance % this.days)/ this.hours);
                const _minutes = Math.floor((distance % this.hours)/ this.minutes);
                const _seconds = Math.floor((distance % this.minutes)/ this.seconds);
                this.displayMinutes = this.format(_minutes);
                this.displaySeconds = this.format(_seconds);
                this.displayHours = this.format(_hours);
                this.displayDays = this.format(_days);
                this.loaded = true
            },1000)
        }
    },
}
</script>

<style>

</style>