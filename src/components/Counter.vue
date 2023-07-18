<template>
    <div class="wrapper grid items-center">
        <section class="text-2xl flex justify-center content-center flex-col mx-auto text-center">Buy Now !
             </section>
        <section class="flex text-6xl justify-center content-center">
            <div class="days mx-2 relative">
                {{displayDays}}
                <div class="label text-sm absolute bottom--1">Days</div>
            </div>
            <span class="leading-sung">:</span>
            <div class="hours mx-3 relative">
                {{ displayHours}}
                <div class="label text-sm absolute bottom--1">Hours</div>
            </div>
            <span class="leading-sung">:</span>
            <div class="minutes mx-3 relative">
                {{ displayMinutes}}
                <div class="label text-sm absolute bottom--1">Minutes</div>
            </div>
            <span class="leading-sung">:</span>
            <div class="seconds ml-3 relative">
                {{ displaySeconds}}
                <div class="label text-sm absolute bottom--1">Seconds</div>
            </div>
        </section>
    </div>
</template>
<script>
export default {
    name: 'CounterVue' , 
    props: ['year' , 'month' , 'date' , 'hour' , 'minute' , 'second' , 'millisecond' ] , 
    data() {
        return {
            displayDays: 0 , 
            displayHours: 0 , 
            displayMinutes: 0 ,
            displaySeconds: 0 , 
        }
    } , 
    computed: { // calculations
        _seconds: () => 1000 , 
        _minutes() {
            return this._seconds * 60
        } , 
        _hours() {
            return this._minutes * 60 ; 
        } ,
        _days() {
            return this._hours * 24 ; 
        } ,
        _end() {
            return new Date(
                this.year , 
                this.month , 
                this.date , 
                this.hour , 
                this.minute , 
                this.second , 
                this.millisecond
            );
        },
        } , 
    

    mounted() {
        this.showRemaining() ; 
    } ,
    methods: {
        showRemaining () {
            const timer = setInterval(() => {
                const now = new Date(); // date of now
                // const end = new Date(2023 , 7 , 9 , 10 , 10 , 10 , 10) ; // the end of the time 
                const distance = this._end.getTime() - now.getTime() ; 

                if (distance < 0) {
                    clearInterval(timer) ; 
                }
                const days = Math.floor(distance / this._days); 
                const hours = Math.floor((distance % this._days) / this._hours) ; 
                const minutes = Math.floor((distance % this._hours) / this._minutes) ; 
                const seconds = Math.floor((distance % this._minutes) / this._seconds) ; 
                this.displayMinutes = minutes < 10 ? "0" + minutes : minutes;
                this.displaySeconds = seconds < 10 ? "0" + seconds: seconds ; 
                this.displayHours = hours < 10 ? "0" + hours:hours ; 
                this.displayDays = days < 10 ? "0" + days:days ;

            }, 1000 );
        }
    }
}
    



</script>
<style >
.seconds {
    max-width: 60px;
}


</style>