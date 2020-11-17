<template>
  <div>
  <div class="box">
    <p class="text">Груповий рейтинг</p>
    <bars class="chart"
          :data="Rating"
          :label-data="Group"
          :gradient="['#f94144', '#ffe74c']"
          :barWidth="30"
          :height="300"

          :max="10"

          label-rotate="0"
          :growDuration="1"></bars>
  </div>
    <div class="box">
      <p class="text">Завдань виконано</p>
      <bars class="chart"
            :data="Tasks"
            :label-data="Group"
            :gradient="['#f94144', '#ffe74c']"
            :barWidth="30"
            :height="300"

            :max="10"
            label-rotate="0"
            :growDuration="1"></bars>
    </div>

  </div>
</template>

<script>
  import Bars from 'vuebars'
  var groupData;
  var rating = new Array();
  var group = new Array();
  var tasks = new Array();
export default {
  name: 'HelloWorld',
  components: {
    Bars
  },
  props: {
    Rating: Array,
    Group:Array,
    Tasks:Array,
  },
  mounted () {
    groupData=new Array(this.getData());
    var interval = setInterval(function() {
      if (groupData[0][1]!=null){
        console.log(groupData[0][1].FinalRating);
        groupData[0].forEach(element => rating.push(element.FinalRating));
        groupData[0].forEach(element => group.push(element.Group));
        groupData[0].forEach(element => tasks.push(element.TaskReceived));
        clearInterval(interval);
      }
    }, 500);
    this.Rating=rating;
    this.Group=group;
    this.Tasks=tasks;
  },

  methods:{
    getData(){
      var finalRating= new Array();
      database.ref('1P4D8W1bSUGsFw0-eZIZd3RhUBM432C7fw6CfUJIVNdk/Rating').once('value',function(querySnapshot) {
        querySnapshot.forEach(function (snapshot) {
          ratingData.push(snapshot.val())
        });
        //ratingData.forEach(element => finalRating.push(element.FinalRating))
        ratingData.forEach(element => finalRating.push(element))

      })
      return finalRating;
    }
  }
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
  color: white;
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
  .table{
    font-size: 2vw;
    margin: auto;
    width: 80vw;
    height: 90%;
    border: white solid 4px;
    border-radius: 20px;
    border-collapse: collapse;
    color: white;
  }
th, td {
  padding: 15px;
  border: white solid 2px;
  border-collapse: inherit;
}

</style>
