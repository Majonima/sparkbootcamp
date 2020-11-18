<template>
  <div id="app">
    <div>
      <div class="box card">
        <p class="text">Груповий рейтинг</p>
        <bars class="chart"
              :data="Rating"
              :label-data="Group"
              :gradient="['#f94144', '#ffe74c']"
              :barWidth="30"
              :height="300"
              :max="10"
              :label-rotate=0
              :growDuration="1"></bars>
      </div>
      <div class="box card">
        <p class="text">Завдань виконано</p>
        <bars class="chart"
              :data="Tasks"
              :label-data="Group"
              :gradient="['#f94144', '#ffe74c']"
              :barWidth="30"
              :height="300"
              :max="6"
              :label-rotate=0
              :growDuration="1"></bars>
      </div>
  </div>
    <div class="base card" v-if="Visible">
      <table width="100%" >
        <tr style="font-size: 1.5vw;">
          <th>Номер</th>
          <th>Завдання</th>
          <th>Оцінювання</th>
        </tr>
        <tr style="font-size: 1vw;" v-bind:key="t" v-for="t in TaskData">
         <th v-if="!t.Visible">{{t.Date}}</th>
          <th  v-if="!t.Visible">{{t.Description}}</th>
          <th v-if="!t.Visible">{{t.Points}}</th>
        </tr>

      </table>
    </div>
  </div>
</template>

<script>
  import Bars from 'vuebars'

export default {
  name: 'App',
  components: {
    Bars
  },
  props: {
    Rating: Array,
    Group:Array,
    Tasks:Array,

    TaskData: Array,
      Visible: Boolean,
  },
  mounted(){
    this.Visible=false;
    this.Rating= new Array;
    this.Group= new Array;
    this.Tasks= new Array;
    this.TaskData= [];
    var that=this;
    this.getData(that);
  },



  methods:{
    getData(context){
      var ratingDb =database.ref('1P4D8W1bSUGsFw0-eZIZd3RhUBM432C7fw6CfUJIVNdk/Rating');
      var tasksDb =database.ref('1P4D8W1bSUGsFw0-eZIZd3RhUBM432C7fw6CfUJIVNdk/Tasks');
      ratingDb.once('value',function(querySnapshot) {
        querySnapshot.forEach(function (snapshot) {
          ratingData.push(snapshot.val())
        });
        ratingData.forEach(element => context.Rating.push(element.FinalRating));
        ratingData.forEach(element => context.Group.push(element.Group));
        ratingData.forEach(element => context.Tasks.push(element.TaskReceived));
      });
      tasksDb.once('value',function(querySnapshot) {
        var key=0;
        querySnapshot.forEach(function (snapshot) {
          context.TaskData[key++]=snapshot.val();
        });
        setTimeout(function(){context.Visible=true; console.log(context.TaskData); },1000)
      })
    }
  },

}
  import firebase from "firebase";
  let ratingData = new Array();
  //let tasksData = new Array();
  //let finalRatig = new Array();
  var config = {
    apiKey: 'AIzaSyCGPNl0TuaHJR898UpNGbW5OBNjdTg6Vl4',
    authDomain: "spark-bootcamp.firebaseapp.com",
    databaseURL: "https://spark-bootcamp.firebaseio.com/",
    projectId: 'spark-bootcamp'
  }

  firebase.initializeApp(config);
  var database= firebase.database();
  /*
  function addProp(key,value){
    ratingData[key]=value;
  }
  */





</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
  .box{
    margin: 0;
    padding: 0;
    margin-left: auto;
    margin-right: auto;
    width: 40vw;
    height: 22vw;
    overflow: visible;
    color: #565656;
    padding-bottom: 2vw;
    display: inline-block;

  }
  .chart{
    margin: 0;
    margin-left: auto;
    margin-right: auto;
    width: 90%;
    height: 90%;
    overflow: inherit;
  }
  .text{
    font-size: 3vw;
    margin: 0;

  }
  .base{
    margin: 0;
    margin-top: 5px;
    padding: 0;
    padding-top: 10px;

    margin-left: auto;
    margin-right: auto;
    width: 80vw;
    min-heightheight: 22vw;
    overflow: visible;
    color: #565656;
    padding-bottom: 2vw;
    display: inline-block;
  }



#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}

table{
  border-spacing: 10px;
  border-collapse: collapse;;
  border:solid white 2px;
}
th{
  min-height: 50vw;
  box-shadow: 0 2px 4px 0 rgba(0,0,0,0.2);
  padding-left: 10px;
  padding-right: 10px;
  padding-top: 5px;
  padding-bottom: 5px;
  font-size: 1vw;
  min-width: 8vw;
}

  .card {
    /* Add shadows to create the "card" effect */
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    transition: 0.3s;
    background: white;
  }

  /* On mouse-over, add a deeper shadow */
  .card:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
  }
  @media screen and (min-width: 320px) and (max-width: 767px) and (orientation: portrait) {

  }
</style>
