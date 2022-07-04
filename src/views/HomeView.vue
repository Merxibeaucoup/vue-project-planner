<template>
  <div class="home">

       <!-- $event is the data being set by -->
              <!-- send current as a prop into the filterNav by data binding-->
                     <!-- current changes everytime we click on a different filter -->


    <FilterNav @filterChange="current = $event"  :current="current"/>

    <!-- shows only if there are elements in projects-->
    <!--- if projects is an empty an array it would be false -->
    <div v-if="projects.length">
      <!--- Cycle through the filteredprojects-->
        <div v-for="project in filteredProjects" :key="project.id">
          <!-- list out the projects -->
                    <!-- @delete ie being emitted from the SingleProject file -->
            <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete"/>
        </div>
    </div>
  </div>
</template>

<script>

import SingleProject from '../components/SingleProject.vue'
import FilterNav from '../components/FilterNav.vue'

export default {
  name: 'HomeView',
  components: {
   SingleProject,
   FilterNav
  },
  data(){
    return{
      //stores all prjects into this array 
      projects: [],
      // the current filter
      current: 'all'
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    // take the response and pass a json
    .then(res => res.json())
    // once we fetch data , array is updated with the data
    .then(data => this.projects = data)
    //catch any error
    .catch(err=> console.log(err.message))
  },
  methods:{
    // if the id of the project that we are cycling through is not equal to the id
    //the this is gomna be true 
    // if the ids are equal this would be false and it will be filtered out
    //the filtered array is been assinged and will no longer contain that id

    handleDelete(id){
        this.projects = this.projects.filter((project) =>{
          return project.id !== id
        })
    },

    // true if id matches the project id
    //stores it inside p
    handleComplete(id){
        let p = this.projects.find(project => {
          return project.id == id
        })
        // update p
        p.complete = !p.complete
    }
  }, 
  computed:{

    // returns the filtered projects 
    filteredProjects(){
      // returns all completed projects
      if(this.current === 'completed'){
        return this.projects.filter(project => project.complete)
      }
      // returns all ongoing projects not completed yet
      if(this.current === 'ongoing'){
        return this.projects.filter(project => !project.complete)
      }

      //returns all projects
      return this.projects
    }
  }
}
</script>
