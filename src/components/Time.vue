<template>
<div>
    <button class="active" v-on:click="checkCity('msc')">Moscow Time</button>
    <button  v-on:click="checkCity('ny')">New York Time</button>

    <p class="time">getGlobalTime2 {{ getGlobalTime() }}</p>
    <p class="time">GlobalTime {{ timeGlobal }}</p>

    <b class="time">Moscow Time {{checkGlobalTime('msc')}}</b> <br>


    <b class="time">NewYork Time {{time}}</b>
    <p class="time">count {{count}}</p>



</div>
</template>

<script>
    import axios from 'axios';
    export default {
        name: "Time",
        data() {
            return {
                state: 'msc',
                status: true,
                date: '',
                timeLocal: null,
                timeGlobal: '',
                timeGlobalcheck: '',
                timer: true,
                // time1: this.setTimer1(),
                // time2: this.setTimer2(),
                results: {},
                c: 0,
                count: 0,
                interval: 0,

            }

        },
        methods: {
                getTime(){

                    //
                },

                checkCity(city) {
                        this.state = city
                },
                addZero(i) {
                    if (i < 10) {
                        i = "0" + i;
                    }
                    return i;
                },
                getCurrentTime1(){

                    let time1 = new Date(Date.now());

                    let h1 = this.addZero(time1.getHours());
                    let m1 = this.addZero(time1.getMinutes());
                    let s1 = this.addZero(time1.getSeconds());
                    this.timeLocal = ((h1).toString() + ":" + (m1).toString() + ':' + (s1).toString()) ;

                },

                getGlobalTime(){
                    var time2 = new Date(this.results);
                    this.timeGlobal = time2;

                    // let h1 = this.addZero(time2.getHours());
                    // let m1 = this.addZero(time2.getMinutes());
                    // let s1 = this.addZero(time2.getSeconds());
                    // let time = ((h1).toString() + ':' + (m1).toString() + ':' + (s1).toString()) ;
                    //console.log(time);

                    //return (time);
                },


                checkGlobalTime() {

                    switch (this.state) {
                        case 'ny' : {
                            this.interval = -8;
                            break;
                        }
                        case 'msc' : {
                            this.interval = 0;
                            break;
                        }
                        default:
                            this.interval = 0;



                    }

                        let time =  this.timeGlobal;

                        time.setHours(time.getHours() + this.interval);
                        time.setSeconds(time.getSeconds() + this.count);


                        let h2 = this.addZero(time.getHours());
                        let m2 = this.addZero(time.getMinutes());
                        let s2 = this.addZero(time.getSeconds());
                        return ((h2).toString() + ':' + (m2).toString() + ':' + (s2).toString()) ;
                       




        },

                // setTimer1() {
                //     return setInterval(this.getCurrentTime1,1000);
                // },
                // setTimer2(){
                //     return setInterval(this.getGlobalTime,1000);
                // },
            counter() {
                    if (this.status) {
                        setTimeout(() => {
                            this.count++;
                            this.counter()
                            }, 1000
                        )
                    }

            },

            },
        incrementTime() {
            this.count = parseInt(this.count) + 1;
        },

            created(){
                axios.get('https://worldtimeapi.org/api/timezone/Europe/Moscow')
                    .then(response => this.results = response.data.datetime);
                this.getGlobalTime();
                //this.getCurrentTime1();
                setInterval(this.getCurrentTime1,1000);
                this.counter();
            },
        computed: {




            // timeNew: function() {
            //     return this.hours + ":" + this.minutes + ":" + this.seconds;
            // },
            // milliseconds: function() {
            //     return this.timeGlobal;
            // },
            // hours: function() {
            //     var milli = this.milliseconds;
            //     // Doing the math
            //      let hrs = Math.floor((milli / 3600000) % 24);
            //     // Using getHours()
            //      //let hrs = new Date().getHours();
            //     if (hrs >= 13) { hrs = hrs - 12 }
            //     return hrs >= 10 ? hrs : '0' + hrs;
            // },
            // minutes: function() {
            //     var milli = this.milliseconds;
            //     var min = Math.floor((milli / 60000) % 60);
            //     return min >= 10 ? min : '0' + min;
            // },
            // seconds: function() {
            //     var milli = this.milliseconds;
            //     var sec = Math.ceil((milli % 60000) / 1000).toFixed(0);
            //     if (sec == 60) { sec == '00' }
            //     return sec >= 10 ? sec : '0' + sec;
           // }
        },

    }

</script>

<style scoped>
button {
    margin: 10px;
    width: 100px;
    height: 30px;
    border: 1px solid #42b983;
    color: #2c3e50;
}
    .active {
        background: aqua;
    }
</style>
