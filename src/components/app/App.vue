<template>
    <div class="app font-monspace">
        <div class="content">
          <AppInfo 
            :allMuviesCount="muvies.length"
            :FavouriteMuviesCount="muvies.filter(muvie => muvie.favourite2).length"
          />
          <div class="search-panel">
              <SearchPanel />
              <AppFilter />
          </div>
          <movie-list :muviesYubor="muvies" />
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
                    favourite2: false,
                    link: true,
                },
                {   
                    id :2,
                    name: 'Shaytanat',
                    viewers: 411,
                    favourite2: false,
                    link: false,
                },
                {   
                    id :3,
                    name: 'Osmodagi bolalar',
                    viewers: 711,
                    favourite2: true,
                    link: false,
                }
            ]
        };
    },
    methods:{
      creatMovieQabul(itme){
        // itme massivga push qilib qoyish 
        this.muvies.push(itme)
        console.log(itme);
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