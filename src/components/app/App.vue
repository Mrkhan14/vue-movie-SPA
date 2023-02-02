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
          <movie-list 
            :muviesYubor="onFiltereHandler(onSoecheHandler(muvies, term), filter)" 
            @onToggle="onToggleHandler"
            @onRemove="onRemoveHandler"
          />
          <movie-app-form  @creatMovie="creatMovieQabul"/>
        </div>
    </div>
</template>
<script>
import AppInfo from "@/components/app-info/AppInfo.vue";
import SearchPanel from '@/components/search-panel/SearchPanel.vue';
import AppFilter from '@/components/app-filter/AppFilter.vue';
import MovieList from '@/components/movie-list/MovieList.vue';
import MovieAppForm from '@/components/movie-app-form/MovieAppForm.vue';
export default {
    components: {
      AppInfo,
      SearchPanel,
      AppFilter,
      MovieList,
      MovieAppForm,
    },
    data() {
        return {
          muvies:[
                {  
                    id :1,
                    name: 'Omar',
                    viewers: 811,
                    favourite: false,
                    like: true,
                },
                {   
                    id :2,
                    name: 'Shaytanat',
                    viewers: 411,
                    favourite: false,
                    like: false,
                },
                {   
                    id :3,
                    name: 'Osmodagi bolalar',
                    viewers: 711,
                    favourite: true,
                    like: false,
                }
          ],
          term:'',
          filter: 'all'
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