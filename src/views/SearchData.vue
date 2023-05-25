<template>
  <div class="w-[95%] sm:w-[80%] lg:w-[1440px] lg:px-[120px]">
    <div class="  mb-20 bg-white flex justify-between items-center rounded-md p-5 shadow-xl">
      <div class="w-[100%] bg-black flex">

        <select class="js-example-basic-multiple w-full" name="states[]" multiple="multiple"  v-model="cariData">
          <option v-bind:value="user.id" :key="user.id" v-for="user in users" >{{  user.company }}</option>
          <option v-bind:value="user.id" :key="user.id" v-for="user in users" >{{  user.position }}</option>
          <option v-bind:value="user.id" :key="user.id" v-for="user in users">{{  user.role }}</option>
          <option v-bind:value="user.id" :key="user.id" v-for="user in users" >{{  user.level }}</option>
          <option v-bind:value="language" v-for="language in users.languages" >{{  language }}</option>
          <option v-bind:value="tool" v-for="tool in users.tools" >{{  tool }}</option>
        </select>
      </div>
      <div class=" pl-5 font-black cursor-pointer" @click="getSelectedOptions">Cari</div>
    </div>


    <div class="data my-[60px] " v-for="data in users">
      <div class="mt-3 py-8 bg-white w-full shadow-xl  rounded-md" :class="{ 'border-l-[5px] border-[#5ba4a4]': data.new && data.featured }">
      
        
        <div class=" lg:hidden foto w-[70px] h-[70px] rounded-full  relative  top-[-60px] mb-[-50px] right-[-20px]"><img :src="'/src/assets/images/' + data.logo" alt=""></div>
        <div class="mx-5 lg:flex lg:justify-end items-center">
            <div class="informasi flex  w-[100%]">
            <div class="w-[100px]  lg:block hidden  mr-5  h-full"><img :src="'/src/assets/images/' + data.logo" alt=""></div>
              <div>
                  <div class="flex items-center  ">
                  <h1 class="   mr-5 text-[18px] primary-color">{{ data.company}}</h1>
                
                  <div class="flex items-center   mr-2 pt-1 px-3 text-white bg-[#5ba4a4] rounded-full" v-if="data.new">NEW!</div>
                  <div class="   mr-2  pt-1 px-3 text-white bg-[#2c3a3a] rounded-full" v-if="data.featured">FEATURED</div>
                
                </div>
                <h1 class="mt-3 text-xl font-semibold">{{data.position}}</h1>
                <div class="flex mt-2 text-gray-400">
                    <h1 class="pr-2">{{data.postedAt}}</h1><div class="w-1 h-1 flex my-auto rounded-full bg-gray-400 mx-2"></div>
                    <h1 class="pr-2 pl-2">{{data.contract}}</h1><div class="w-1 h-1 flex my-auto rounded-full bg-gray-400 mx-2"></div>
                    <h1 class="pr-2 pl-2">{{data.location}}</h1>
                </div>
              </div>
              
            </div>
            <hr class=" lg:hidden border-gray-400 border-1 my-5">

            <div class="skills  flex  w-full flex-wrap lg:justify-end ">
              <div class="text-lg py-1 px-3 font-[600] text-[#5ba4a4] mr-3 my-2 bg-[#eef6f6] rounded-md ">{{ data.role }}</div>
              <div class="text-lg py-1 px-3 font-[600] text-[#5ba4a4] mr-3 my-2 bg-[#eef6f6] rounded-md ">{{ data.level }}</div>
              <div class="text-lg py-1 px-3 font-[600] text-[#5ba4a4] mr-3 my-2 bg-[#eef6f6] rounded-md " v-for="language in data.languages" :key="language">{{ language }}</div>
              <div class="text-lg py-1 px-3 font-[600] text-[#5ba4a4] mr-3 my-2 bg-[#eef6f6] rounded-md " v-for="tool in data.tools" :key="tool">{{ tool }}</div>


            
            </div>
        </div>

        
      </div>
    </div>

 

  </div>
</template>

<style>
/* ### Primary

- Desaturated Dark Cyan: hsl(180, 29%, 50%)

### Neutral

- Light Grayish Cyan (Background): hsl(180, 52%, 96%) / 	#effafa
- Light Grayish Cyan (Filter Tablets): hsl(180, 31%, 95%) / #eef6f6
- Dark Grayish Cyan: hsl(180, 8%, 52%)
- Very Dark Grayish Cyan: hsl(180, 14%, 20%) / 	#2c3a3a*/
.primary-color {
  color: #5ba4a4;
}

body {
  background-color: hsl(180, 52%, 96%);
}
.select2-selection__choice{
  background-color: red;
}
.select2-container--default .select2-selection--multiple .select2-selection__choice {
  background-color: red;
}
.select2-container--default .select2-selection--multiple .select2-selection__choice__remove {
  position: relative;
  right: 0;
  top: 0;
  
}
</style>

<script>
import jsonData from '../../data.json';


export default {
  data() {
    return {
      users: [],
      cariData: [],
      selectedItems: [],
      
    };
  },
  mounted() {
    this.users = jsonData.users;

  }, methods: {
    getSelectedOptions() {
      console.log(this.cariData);
    },
  }
  
};

$(document).ready(function() {
    $('.js-example-basic-multiple').select2();
});
</script>