<template>

  <div id="app">
    <main>
      <div class="inputBox">
        <input type="text" class="inputField" :class="{shake:shaking}" placeholder="input weight here..." v-model="inputWeight"/>
      </div>
      <div class="calculateBtnBox">
        <button class="calculateBtn" @click="calculateOnClick">calculate</button>
      </div>

       <div class="weightSection">
        <div class="weight" id="emptyBar"></div>
        <!--
        <div class="plates" id="twenty-five">25</div>
        <div class="plates" id="twenty">20</div>
        <div class="plates" id="fifteen">15</div>
        <div class="plates" id="ten">10</div>
        <div class="plates" id="five">5</div>
        <div class="plates" id="two-point-five">2.5</div>
        <div class="plates" id="one-point-two-five">1.25</div>
      -->
        <div v-for="plate in plates" :key="plate.id" :id="plate.id" class="plates">{{plate.value}}</div>


      </div>

    <div class="info">
      Per side: {{perside}} kg
    </div>
    <div class="info2">
      Unmountable weight(each side): {{unmounted}} kg
    </div>
    
    </main>
  </div>
</template>

<script>

export default {
  name: "App",
  data(){
    return{
      inputWeight:'',
      perside:0,
      smallestDenomination:1.25,
      biggestDenomination:20,
      barWeight: 20,
      plates: [],
      unmounted:0,
      shaking: false,
      denominations:[
        {
          id:"twenty-five",
          value: 25,
          enabled: false
        },
        {
          id:"twenty",
          value: 20,
          enabled: true
        },
        {
          id:"fifteen",
          value: 15,
          enabled: true
        },
        {
          id:"ten",
          value: 10,
          enabled: true
        },
        {
          id:"five",
          value: 5,
          enabled: true
        },
        {
          id:"two-point-five",
          value: 2.5,
          enabled: true
        },
        {
          id:"one-point-two-five",
          value: 1.25,
          enabled: true
        }   
      ]
    }
  },
  methods:{

    calculateOnClick(){
        if(this.inputWeight != '' && this.inputWeight >= (this.smallestDenomination + this.smallestDenomination + this.barWeight)){
          this.plates = []
          this.calculatePerSide()
          this.setDenominations()
        }else{
          this.shakeInputBox()
        }
        
    },

    calculatePerSide(){
      this.perside = (this.inputWeight - this.barWeight)/2
    },

    setDenominations(){

      let temp = this.perside
  

      for(let i =0;i<this.denominations.length;i++){

        while(this.denominations[i].value <= temp && this.denominations[i].enabled){
            temp -= this.denominations[i].value
            this.plates.push(this.denominations[i])
        }

      }
   
      this.unmounted = temp
      
    },

    shakeInputBox() {
      this.shaking = true
      setTimeout(() => {
        this.shaking = false
      }, 1500)
    }



  }
};
</script>

<style>
* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  width:100%;
  height: 100%;
  overflow:hidden;
}

body {
  font-family: "montserrat", sans-serif;

}

#app {
  background-image: url("./assets/bg.jpg");
  background-size: 100% 100%;

}




main {

  background-image: linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 1));
}

.inputBox{
  margin:auto;
  margin-top:65%;
  width: fit-content;
  height: fit-content;

}

.inputField{
  text-align: center;
  border-radius: 7px;
  height: 50px;
  outline: none;
  border: none;
  background-color: rgba(0, 0, 0, 0.7);
  color: white;
}


.calculateBtnBox{
  margin-top: 20px;
  text-align: center;
  height: fit-content;
}
.calculateBtn{
  height:40px;
  width: 80px;
  border-radius: 10px;
  border: none;

}

.calculateBtn:active{
  background-color:#3e8e41;
}

.weightSection{

  margin-top: 10%;
  height: fit-content;
  display: flex;
  justify-content: center;
  align-items: center;
}

#emptyBar{
  background-color: rgb(119, 116, 116);
  height: 10px;
  width: 100px;
}


#twenty-five{
  height: 120px;
  background-color: red;
}

#twenty{
  height: 120px;
  background-color: blue;
}

#fifteen{
  height: 100px;
  background-color: rgb(221, 221, 20);
}

#ten{
  height: 80px;
  background-color: green;
}

#five{
  height: 60px;
  background-color: rgb(196, 186, 169);
}

#two-point-five{
  height: 40px;
  background-color: black
}

#one-point-two-five{
  height: 30px;
  background-color: rgb(192, 182, 166);
}

.plates{
  width: 17px;
  font-size: 12px;
  color: white;
  writing-mode: vertical-rl;
  text-orientation: sideways;
  padding:3px;
  border-radius: 7px;
  border: 1px solid black;
}

.info{
  margin-top: 40px;
  color: white;
  text-align: center;
  height: fit-content;
}

.info2{
  margin-top: 10px;
  color: white;
  text-align: center;
  height: fit-content;

}

.shake {
  animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
  transform: translate3d(0, 0, 0);
}


@keyframes shake {
  10%,
  90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%,
  80% {
    transform: translate3d(2px, 0, 0);
  }

  30%,
  50%,
  70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%,
  60% {
    transform: translate3d(4px, 0, 0);
  }
}

@media only screen and (min-width: 600px){
  .inputBox{
  margin:auto;
  margin-top:15%;
  width: fit-content;
  height: fit-content;
}

.weightSection{

  margin-top: 3%;
  height: fit-content;
  display: flex;
  justify-content: center;
  align-items: center;
}
}

</style>
