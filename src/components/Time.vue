<template>
<div>
    <button :class="[state === 'msc' ? 'active' : '']"  v-on:click="checkCity('msc')">Moscow Time</button>
    <button :class="[state === 'ny'  ? 'active' : '']"  v-on:click="checkCity('ny')">New York Time</button>

    <div class="time" v-if="state === 'msc' "><b>Moscow Time </b>{{checkGlobalTime()}}</div>
    <div class="time" v-if="state === 'ny' "><b>New York Time </b>{{checkGlobalTime()}}</div>
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
                timeGlobal: '',
                results: {},
                count: 0,
                interval: 0,
            }

        },
        methods: {

                checkCity(city) {
                        this.state = city
                },
                addZero(i) {
                    if (i < 10) {
                        i = "0" + i;
                    }
                    return i;
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
                        let time = new Date(this.results);
                        time.setHours(time.getHours() + this.interval);
                        time.setSeconds(time.getSeconds() + this.count);
                        let h2 = this.addZero(time.getHours());
                        let m2 = this.addZero(time.getMinutes());
                        let s2 = this.addZero(time.getSeconds());
                        return ((h2).toString() + ':' + (m2).toString() + ':' + (s2).toString()) ;
                },

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

        beforeCreate() {
                axios.get('https://worldtimeapi.org/api/timezone/Europe/Moscow')
                    .then(response => this.results = response.data.datetime);
            },
        created() {
                this.counter();
        }
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
