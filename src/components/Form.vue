<template>
    <form @submit.prevent="hideform">
        <textarea class='txt'>You don't have enough MANA or ACTION POINTS</textarea>
        <button class='btn' @click.prevent="hideform">ok</button>
    </form>
</template>

<script>
    //import Hero from './Hero';
    export default {
        name: 'Form',
        components: {
            //Hero,
        },
        props: {
            manaAp:{
                type: Boolean,
                value: false
            }
        },
        methods: {
            hideform() {
                this.manaAp = false;
                this.$emit('hideform');
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