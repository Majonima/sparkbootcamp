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

              :max="10"
              :label-rotate=0
              :growDuration="1"></bars>
      </div>
  </div>
    <div class="base card">
      <table width="100%">
        <tr>
          <th>Номер</th>
          <th>Завдання</th>
          <th>Оцінювання</th>
        </tr>

      </table>
    </div>
  </div>
</template>

<script>
  import Bars from 'vuebars'
  var groupData;
  var taskData;
  var rating = new Array();
  var group = new Array();
  var tasks = new Array();
 // var taskNumber = new Array();
 // var task = new Array();
 // var taskValue = new Array();

export default {
  name: 'App',
  components: {
    Bars
  },
  props: {
    Rating: Array,
    Group:Array,
    Tasks:Array,
    TaskNumber : Array,
    Task : Array,
    TaskValue : Array,
    TaskData: Array
  },
  mounted () {
    groupData=new Array(this.getData('Rating'));
    taskData= new Array(this.getData('Tasks'));

    var interval = setInterval(function() {
      if ((groupData[0][1]!=null)){
        console.log(groupData[0][1].FinalRating);
        groupData[0].forEach(element => rating.push(element.FinalRating));
        groupData[0].forEach(element => group.push(element.Group));
        groupData[0].forEach(element => tasks.push(element.TaskReceived));
        console.log(taskData[0])

        /*
        taskData[0].forEach(element => taskNumber.push(element.Task));
        taskData[0].forEach(element => task.push(element.Description));
        taskData[0].forEach(element => taskValue.push(element.Points));
        */
        clearInterval(interval);
      }
    }, 500);
    this.Rating=rating;
    this.Group=group;
    this.Tasks=tasks;
  },

  methods:{
    getData(key){
      var innerData= new Array();
      database.ref('1P4D8W1bSUGsFw0-eZIZd3RhUBM432C7fw6CfUJIVNdk/'+key).once('value',function(querySnapshot) {
        querySnapshot.forEach(function (snapshot) {
          ratingData.push(snapshot.val())
        });
        //ratingData.forEach(element => finalRating.push(element.FinalRating))
        ratingData.forEach(element => innerData.push(element))
      })
      return innerData;
    }
  },

}
  import firebase from "firebase";
  let ratingData = new Array();
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
    padding: 0;
    margin-left: auto;
    margin-right: auto;
    width: 80%;
    height: 90%;
    overflow: inherit;
  }
  .text{
    font-size: 3vw;
    margin: 0;

  }
  .base{
    margin: 0;
    margin-top: 10px;
    padding: 0;
    padding-top: 10px;

    margin-left: auto;
    margin-right: auto;
    width: 80vw;
    height: 22vw;
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
body{
  background-color: black;
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

</style>
