<template>

  <div class="w-[95%] sm:w-[80%] lg:w-[1440px] lg:px-[120px]">
    <div class="mb-20 bg-white flex justify-between items-center rounded-md p-5 shadow-xl">
      <div class="w-[100%]  flex">
        <Multiselect
          v-model="cariData"
          mode="tags"
          :close-on-select="false"
          :searchable="true"
          :create-option="true"
          :options="formattedOptions"
          :multiple="true"
          :taggable="true"
          placeholder="Cari data..."
        />
      </div>
    </div>

    <!-- <h1>{{ cariData }}</h1> -->


    <div class="data my-[60px] " v-for="data in filteredUsers" :key="data.id">
      <div class="mt-3 py-8 bg-white w-full shadow-xl  rounded-md" :class="{ 'border-l-[5px] border-[#5ba4a4]': data.new && data.featured }">
      
        
       
        <div class="mx-5 lg:flex lg:justify-end items-center">
            <div class="informasi flex  w-[100%]">
            <img :src="'./assets/' + data.logo" class="w-[70px]  lg:w-[100px] lg:relative absolute lg:mt-0 mt-[-60px]  mr-5  h-full">
              <div>
                  <div class="flex items-center  mt-5 lg:mt-0">
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

<style src="@vueform/multiselect/themes/default.css"></style>

<script>
import jsonData from '../../data.json';
import Multiselect from '@vueform/multiselect'


export default {
  components: {
      Multiselect,
    },
  data() {
    return {
      users: [],
      cariData: []
    };
  },
  mounted() {
    this.users = jsonData.users;

  },
  computed: {
    filteredUsers() {
      if (this.cariData.length === 0) {
        // Jika tidak ada filter yang dipilih, tampilkan semua pengguna
        return this.users;
      } else {
        // Filter pengguna berdasarkan filter yang dipilih
        return this.users.filter(user => {
          // Periksa apakah setiap filter cocok dengan data pengguna
          return this.cariData.every(filter => {
            return (
              user.company.includes(filter) ||
              user.position.includes(filter) ||
              user.role.includes(filter) ||
              user.level.includes(filter) ||
              user.languages.some(language => language.includes(filter)) ||
              user.tools.some(tool => tool.includes(filter))
            );
          });
        });
      }
    },
    formattedOptions() {
      // Mengambil opsi untuk dropdown Multiselect
      const options = [];
      this.users.forEach(user => {
        options.push({
          label: user.company,
          value: user.company
        });
        options.push({
          label: user.position,
          value: user.position
        });
        options.push({
          label: user.role,
          value: user.role
        });
        options.push({
          label: user.level,
          value: user.level
        });
        user.languages.forEach(language => {
          options.push({
            label: language,
            value: language
          });
        });
        user.tools.forEach(tool => {
          options.push({
            label: tool,
            value: tool
          });
        });
      });
      return options;
    }
  },
  methods: {
    getSelectedOptions() {
      console.log(this.cariData);
    }
  }
};

$(document).ready(function() {
    $('.js-example-basic-multiple').select2();
});
</script>