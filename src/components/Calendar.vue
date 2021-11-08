<template>
<div class="m-auto">
  <h1 class="text-2xl my-2 text-center">Vue Calendar</h1>
  <section class="mx-2 flex justify-between">
      <h2 class="font-bold">{{currentMonthName}}</h2>
      <h2 class="font-bold">{{currentYear}}</h2>
  </section>
  <section class="flex">
      <p v-for="day in days" :key="day" class="text-center" style="width: 14.28%">{{day}}</p>
  </section>
  <section class="flex flex-wrap">
      <!-- Printing blank <p> depending on the start day -->
      <p v-for="num in startDay()" :key="num" class="text-center" style="width: 14.28%"></p>
      <p v-for="num in daysInMonth()" :key="num" class="text-center" style="width: 14.28%" :class="currentDateClass(num)">{{num}}</p>
  </section>
  <section class="flex justify-between my-2">
      <button class="px-2 border rounded" @click="prev()">Prev</button>
      <button class="px-2 border rounded" @click="next()">Next</button>
  </section>
</div>
  
</template>

<script>
export default {

    data(){
        return{
            currentDate: new Date().getDate(),
            days: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
            currentYear: new Date().getFullYear(),
            //This method return the month in string -> currentMonth: new Date().toLocaleString('default',{month: 'long'})
            currentMonth: new Date().getMonth() +1
        }
    },
    methods:{
        daysInMonth(){
            // const month = new Date().getMonth()+1
            return new Date(this.currentYear, this.currentMonth, 0).getDate()
        },
        //This function will return the index day in the calendar where we have to start in the calendar.
        startDay(){
            return new Date(this.currentYear, this.currentMonth - 1).getDay()
        },
        next(){
            if(this.currentMonth === 12){
                this.currentMonth = 0 + 1
                this.currentYear++
            }else{
                this.currentMonth++
            }
        },
        prev(){
            if(this.currentMonth===1){
                this.currentMonth=11+1
                this.currentYear--
            }else{
                this.currentMonth--
            }
        },
        currentDateClass(num){
           
          const calendarFullDate = new Date(this.currentYear, this.currentMonth-1, num).toDateString()
          const currentFullDate = new Date().toDateString()
            return  calendarFullDate === currentFullDate ? 'text-yellow-600':'';
        }
    },
    computed:{
        currentMonthName(){
            return new Date(this.currentYear, this.currentMonth -1).toLocaleString('default',{month: 'long'})
        }
    }

}
</script>

<style>

</style>