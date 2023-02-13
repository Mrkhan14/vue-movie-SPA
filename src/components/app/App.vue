<template>
    <div class="app font-monspace">
      
        <div class="content">
          <AppInfo 
            :allMuviesCount="muvies.length"
            :FavouriteMuviesCount="muvies.filter(muvie => muvie.favourite).length"
          />
          <div class="search-panel">
              <SearchPanel :updateTermHandler="updateTermHandler"/>
              <AppFilter   :updateFiltereHandler="updateFiltereHandler" :filterName="filter"/>
          </div>
          
          <card-my v-if="!muvies.length && !isLoading">
              <p class="text-center fs-3 text-danger">Kinolar hozircha yo'q</p>
          </card-my>
          <card-my v-else-if="isLoading">
            <loading ></loading>
          </card-my>
          <movie-list 
            v-else
            :muviesYubor="onFiltereHandler(onSoecheHandler(muvies, term), filter)" 
            @onToggle="onToggleHandler"
            @onRemove="onRemoveHandler"
          />
          <movie-app-form  @creatMovie="creatMovieQabul"/>
        </div>
        <!-- <primary-button @click="fetchMuvies">click</primary-button> -->
    </div>
</template>
<script>
import AppInfo from "@/components/app-info/AppInfo.vue";
import SearchPanel from '@/components/search-panel/SearchPanel.vue';
import AppFilter from '@/components/app-filter/AppFilter.vue';
import MovieList from '@/components/movie-list/MovieList.vue';
import MovieAppForm from '@/components/movie-app-form/MovieAppForm.vue';
import PrimaryButton from '@/ui-components/PrimaryButton.vue';
import Loading from '../../ui-components/Loading.vue';
import axios from 'axios';

export default {
    components: {
      AppInfo,
      SearchPanel,
      AppFilter,
      MovieList,
      MovieAppForm,
      PrimaryButton,
      Loading,
    },
    data() {
        return {
          muvies:[],
          term:'',
          filter: 'all',
          isLoading: false,
        };
    },
    methods:{
      creatMovieQabul(itme){
        // itme massivga push qilib qoyish 
        this.muvies.push(itme)
        console.log(itme);
      },
      onToggleHandler({id, prop}){
        // console.log(prop);
       this.muvies = this.muvies.map(item => {
          if (item.id == id) {
              return{...item, [prop]: !item[prop]}
          }
          return item
        })
      },
      onRemoveHandler(id){
        this.muvies = this.muvies.filter(c => c.id !== id)
      },
      onSoecheHandler(arr, term){
        if (term.length == 0) {
          return arr
        }
        return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1)
      },
      onFiltereHandler(arr, filter){
          switch (arr, filter) {
            case 'popular':
              return arr.filter(c => c.like)
            case 'mostViewers':
              return arr.filter(c => c.viewers > 500)
            default:
              return arr
          }
      },
      updateTermHandler(term){
        // debugger;
        this.term = term
      },
      updateFiltereHandler(filter){
        this.filter = filter 
      },
      
      async fetchMuvies(){
        this.isLoading = true;
        try {
          const {data} = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
          const newArr = data.map(item => ({
            id: item.id,
            name: item.title,
            like: false,
            favourite: false,
            viewers: item.id * 10, 
          }))
          this.muvies = newArr;
          // console.log(newArr);
          }
        catch (error) {
          alert(error.message);
        }
        finally{
          this.isLoading = false;
        }
      },    
    },
    mounted() {
      this.fetchMuvies()
    },


}
</script>

<style>
.app{
  height: 100vh;
  color: #000;
}
.content{
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0px auto;
  padding: 5rem 0;
}
.search-panel{
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>