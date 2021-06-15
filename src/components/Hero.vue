<template>
    <div>
    <div class='two_pics'>
      <div>
        <h1 class='herotext'>Hero</h1>
        <span class="main">
            <img alt="Hero"
                class="hero_pic" 
                src="https://blzmedia-a.akamaihd.net/d3/media/artwork/artwork-class-crusader07-large.jpg"
            >
            <span class="actionbtns">
                <button @click="attckBtn">Attack: <br> deal 5-12 dmg <br> cost 1ap</button>
                <button @click="healBtn">Heal: <br> heal 15 <br>cost 10mana and 1ap</button>
                <button @click="fireballBtn">Fireball: <br>deal 15-30 dmg<br> cost 20mana and 2ap</button>
            </span>
        </span>
        <p class='hp'>Health: <strong>{{modelValue.heroHealthCounter}}</strong> / 100</p>
        <p class='mp'>Mana: <strong>{{modelValue.heroManaCounter}}</strong> / 200</p>
        <p class='ap'>Action Points: <strong>{{modelValue.heroActionPoints}}</strong> / 3</p>
      </div>
    </div>
        <Form class='form' v-show="manaAp" @hideform = 'hideform'/>
        <FormEnd class='form' v-show="turnEnd" @hideformend = 'hideformend'/>
    </div>
</template>

<script>
import FormEnd from './FormEnd'
import Form from './Form'
export default {
    data() {
        return {
            manaAp: false,
            turnEnd: false,
        }
    },
    name: 'hero',
    components: {
        Form, FormEnd
    },
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
        destroyForm() {
            this.manaAp = false,
            this.turnEnd = false
        },
        hideform() {
            this.manaAp = false
        },
        hideformend() {
            this.turnEnd = false
        },
        youWon() {
            alert('you WON! New game Starts');
            this.modelValue.heroActionPoints += 3 - this.modelValue.heroActionPoints;
            this.modelValue.heroHealthCounter += 100+(-this.modelValue.heroHealthCounter);
            this.modelValue.heroManaCounter += 200 - this.modelValue.heroManaCounter;
            this.modelValue.enemyHealthCounter += 200-this.modelValue.enemyHealthCounter;
            setTimeout(this.destroyForm(), 500);
        },
        youLost() {
            //this.modelValue.heroHealthCounter === this.modelValue.heroHealthCounter;
            alert('you LOST! New game Starts');
            this.modelValue.heroActionPoints === 3;
            this.modelValue.heroHealthCounter += 100+(-this.modelValue.heroHealthCounter);
            this.modelValue.heroManaCounter += 200 - this.modelValue.heroManaCounter;
            this.modelValue.enemyHealthCounter += 200-this.modelValue.enemyHealthCounter;
            setTimeout(this.destroyForm(), 500);
        },
        endOfTurn() {
            this.turnEnd = true;
            //alert('your turn has ended. Enemy hits you');
            this.modelValue.heroHealthCounter -= Math.floor(Math.random() * (40 - 14)) + 14;
            this.modelValue.heroActionPoints += 3;
        },
        attckBtn() {
            if(this.modelValue.heroActionPoints > 0) {
                this.modelValue.enemyHealthCounter -= Math.floor(Math.random() * (12 - 5)) + 5;
                this.modelValue.heroActionPoints -= 1;
            }
            if(this.modelValue.enemyHealthCounter <=0 ) {this.modelValue.youWon}
        },
        fireballBtn() {
            if(this.modelValue.heroActionPoints === 1 || this.modelValue.heroManaCounter < 20) {
                this.manaAp = true;
                //alert('you dont have enough action points OR mana')
            }
            else if(this.modelValue.heroActionPoints > 1 && this.modelValue.heroManaCounter >= 20) {
                this.modelValue.heroActionPoints -= 2;
                this.modelValue.heroManaCounter -=20;
                this.modelValue.enemyHealthCounter -= Math.floor(Math.random() * (30 - 15)) + 15;
            }
        },
        healBtn() {
            if(this.modelValue.heroManaCounter < 10) {
                this.modelValue.heroManaCounter===this.modelValue.heroManaCounter
                alert('you dont have enough mana')
            }
            else if(this.modelValue.heroHealthCounter<=85) { 
                this.modelValue.heroHealthCounter+=15;
                this.modelValue.heroManaCounter-=10;
                this.modelValue.heroActionPoints-=1;
            }
            else if (this.modelValue.heroHealthCounter < 100 && this.modelValue.heroHealthCounter > 85) {
                this.modelValue.heroHealthCounter+=100-this.modelValue.heroHealthCounter;
                this.modelValue.heroManaCounter-=10;
                this.modelValue.heroActionPoints-=1
            }
            else if (this.modelValue.heroHealthCounter===100) {
                alert('your hp is full')
            }
        },
    },
    watch: {
        // async 'modelValue.heroHealthCounter'(val) {
        //     if(val <= 0) {
        //         await this.$nextTick();
        //         await this.$nextTick();
        //         this.youLost();
        //     }
        // },
        'modelValue.heroHealthCounter'(val) {
            if(val <= 0) {
                setTimeout(this.youLost, 1000);
            }
        },
        'modelValue.heroActionPoints' (v) {
            if (v <= 0) {
                this.$nextTick(() => {
                    this.endOfTurn()
                })
            }
        },
        'modelValue.enemyHealthCounter'(val) {
            if(val <= 0) {
                this.$nextTick().then(() => {
                    setTimeout(this.youWon, 1000);
                })
            }
        }
    }
}
</script>

<style scoped>
.form {
    display: flex;
    float: right;
}
.ap{
    color: orange;
}
.hp{
    color: green;
}
.mp{
    color: blue;
}
.pp{
    text-align: right;
    color: red;
}
.actionbtns{
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
button{
    width: 100px;
    height: 100px;
    border-radius: 50%;
    margin-left: 10px;
    margin-top: 10px;
    margin-bottom: 10px;
    margin-right: 10px;
}
.main{
    display: flex;

}
.hero_pic {
    display: flex;
    justify-content: left;
    width: 300px;
    height: 400px;
}
.herotext{
    margin: 0;
    justify-content: right;
}
.two_pics{
  display: flex;
  justify-content: space-between;
}
</style>>