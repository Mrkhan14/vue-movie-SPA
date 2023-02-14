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

          <card-my class="d-flex justify-content-center">
            <nav aria-label="pagination">
              <ul class="pagination pagination-lg">
                <li 
                  v-for="pageNumber in totalPages"
                  :key="pageNumber"
                  class="page-item" 
                  @click="changePageHandler(pageNumber)"
                  :class="{'active': pageNumber === page}">
                  <span class="page-link">{{ pageNumber }}</span>
                </li>
              </ul>
            </nav>
          </card-my>
          

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
          limit: 10,
          page:1,
          totalPages: 0,
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
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts',{
            params:{
              _limit: this.limit,
              _page: this.page,
            }
          });
          const newArr = response.data.map(item => ({
            id: item.id,
            name: item.title,
            like: false,
            favourite: false,
            viewers: item.id * 10, 
          }))
          // 100 : 10 = 10 agar qoldiq qolsa u ham bitta pages bo'ladi 101 : 10 = 11
          this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
          this.muvies = newArr;
          console.log(this.totalPages);
          }
        catch (error) {
          alert(error.message);
        }
        finally{
          this.isLoading = false;
        }
      },  
      changePageHandler(page){
        this.page = page       
      },  
    },
    mounted() {
      this.fetchMuvies()
    },
    // kuzatuchi bizni datalarmiz o'zgarsan  return ishdagi  shundan watch ichdagi funksiya ishga tushadi 
    watch:{
      page(){
        this.fetchMuvies();
      }
    }


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