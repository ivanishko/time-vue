<template>
<div>

    <p class="date">{{ date }}</p>
    <p class="time">{{ time1 }}</p>
    <p class="time">{{ time2 }}</p>
    <p class="time">{{ results }}</p>
    <p class="text">ЦИФРОВЫЕ ЧАСЫ с Vue.js</p>

</div>
</template>

<script>
    import axios from 'axios';
    export default {
        name: "Time",
        data() {
            return {
                date: '',
                time: '',
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
                    var time1, h1, m1,s1;
                    time1 = new Date(Date.now());

                    h1 = time1.getHours();
                    m1 = time1.getMinutes();
                    s1 = time1.getSeconds();
                    let time = (toString(h1 + 2) + ':' + toString(m1) + ':' + toString(s1)) ;
                    //console.log(time);
                    return time;
                },
                getCurrentTime2(){
                    var time2, h2, m2,s2;
                    time2 = new Date(this.results);

                    h2 = time2.getHours();
                    m2 = this.addZero(time2.getMinutes());
                    s2 = this.addZero(time2.getSeconds());
                    let time = (`${h2}':'${m2}':'${s2}`) ;
                    console.log(time);
                    return (time);
                },



                setTimer1() {
                    return setInterval(this.getCurrentTime1,1000);
                },
                setTimer2(){
                    return setInterval(this.getCurrentTime2,1000);
                },

            },
            created() {
                axios.get('https://worldtimeapi.org/api/timezone/Europe/Moscow')
                    .then(response => this.results = response.data.datetime)
            }

    }

</script>

<style scoped>

</style>
