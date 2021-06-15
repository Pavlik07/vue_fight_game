<template>
    <form @submit.prevent="hideformend">
        <textarea class='txt'>Your turn has ended, enemy attacked you!</textarea>
        <button class='btn' @click.prevent="hideformend">ok</button>
    </form>
</template>

<script>
    //import Hero from './Hero';
    export default {
        name: 'FormEnd',
        components: {
            //Hero,
        },
        props: {
            turnEnd:{
                type: Boolean,
                value: false
            },
        },
        methods: {
            hideformend() {
                this.turnEnd = false;
                this.$emit('hideformend');
            }
        }
    }
</script>

<style scoped>
.txt{
    background-color: indianred;
}
.btn{
    background-color: greenyellow;
}
</style>