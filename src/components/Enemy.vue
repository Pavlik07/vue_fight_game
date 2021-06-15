<template>
    <div>
        <h1 class='enemytext'>Enemy</h1>
        <span class="main">
            <img alt="Enemy"
                class="enemy_pic" 
                src="https://funpay.ru/img/circles/diablo_3-2.jpg"
            >
        </span>
        <p class="pp">Health: <strong>{{modelValue.enemyHealthCounter}}</strong> / 200</p>
    </div>
</template>

<script>
export default {
    name: 'enemy',
    props: {
        modelValue: {
            type: Object,
        }
    },
    model: {
        prop: 'modelValue',
        event: 'change',
    },
    methods: {
        atckBtn(){}
    }
}
</script>

<style scoped>
.main{
    display: flex;
    justify-content: right;
    float: right;
}
.enemy_pic {
    width: 300px;
    height: 400px;
    margin-bottom: 15px;
}
.enemytext{
    margin: 0;
    text-align: right;
}
p{
    text-align: right;
}
.pp{
    color: red;
}
</style>>