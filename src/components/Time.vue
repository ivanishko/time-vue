<template>
<div>

    <p class="time">time{{ timeLocal }}</p>
    <p class="time">results{{ results }}</p>
    <p class="time">getGlobalTime2 {{ getGlobalTime() }}</p>
    <p class="time">GlobalTime {{ timeGlobal }}</p>


</div>
</template>

<script>
    import axios from 'axios';
    export default {
        name: "Time",
        data() {
            return {
                date: '',
                timeLocal: '',
                timeGlobal: '',
                timer: true,
                time1: this.setTimer1(),
                time2: this.setTimer2(),
                results: {}
            }

        },
        methods: {
                getTime(){

                    //
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
                    let h2 = this.addZero(time2.getHours());
                    let m2 = this.addZero(time2.getMinutes());
                    let s2 = this.addZero(time2.getSeconds());
                    let time = ((h2).toString() + ':' + (m2).toString() + ':' + (s2).toString()) ;
                    //console.log(time);

                    return (time);
                },

                // checkGlobalTime() {
                //     setTimeout(function () {
                //         let time = new Date(this.results);
                //         this.timeGlobal = time.setTime(time.getTime + 1)
                //         }
                //
                //         ,1000)
                //
                //
                // },





                setTimer1() {
                    return setInterval(this.getCurrentTime1,1000);
                },
                setTimer2(){
                    return setTimeout(this.getGlobalTime,1000);
                },

            },

            mounted() {
                axios.get('https://worldtimeapi.org/api/timezone/Europe/Moscow')
                    .then(response => this.results = response.data.datetime);
            }

    }

</script>

<style scoped>

</style>
