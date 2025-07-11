<script setup>

import { ref, useTemplateRef, onMounted } from 'vue';
import { galleryList } from './Scripts/arrayList';


 
//will help us loop through the array of gallery that contains out information
const currentArrayIndex = ref(0);
//display which image we are on to the user
const currentSelection = ref (1);

const showDescription = ref(false);


/* this function moves through the list of pictures in the gallery 
the condition allow the user to move the gallery as long as the current array index is 
not equal to the gallery length - 1 

the reason behind it is that the index is 0 and the gallery length is 5 
the index of the last element is 4 which is the end of the array.

to prevent user from moving passed the last i had to take the array length - 1 which gives me 4 
once the user is on the last item of the array it will prevent the user from moving forward

*/
function MoveFoward(){
if(currentArrayIndex.value != (galleryList.length - 1)){
  currentSelection.value +=1
currentArrayIndex.value +=1
}
}
/* 
this function allows the user to move back to the previous image in the gallery 
once the current array index is not 0 which is the first element the use can move backwards
once the current array index is 0, it the end of the line for the user, the user must move foward now
*/
function MoveBackward(){
if (currentArrayIndex.value != 0){
   currentSelection.value -=1
currentArrayIndex.value -=1
}
}


/* show the description of the current image  */
function description(){
  console.log(showDescription.value);
  showDescription.value = !showDescription.value;
}

</script>

<template>
  <div id="title-container">
  <h2>Vue Gallery</h2>
  </div>
  <div id="button-container">
    <button v-on:click="MoveBackward()">Back</button><button v-on:click="MoveFoward()">Next</button>
  </div>
  <br>
  <br>
 <div id="gallery-container" v-for="(item, index) in galleryList">
<div id="currentImage-container" v-show="currentArrayIndex == 0 ? index == 0: index == currentArrayIndex "> 
<p>{{currentSelection}} of {{ galleryList.length }}</p>
<br>
<img :src="item.image" alt="" id="Image" >
<br>
<br>
<button @click="description()" v-show="!showDescription">Show Description</button>
<button @click="description()" v-show="showDescription">Hide Description</button>
<p v-show="showDescription">{{ item.description }}</p>
</div>
 </div>

</template>

<style scoped>
#title-container{
  text-align: center;
}

#button-container button:nth-child(2){
margin-left: 50px;
}

#button-container button{
  padding: 5px;
  border-radius: 2px;
}

#Image{
height: 350px; 
width: 400px;
}

</style>
