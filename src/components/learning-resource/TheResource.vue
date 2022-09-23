<template>
<div>
  <base-card>
    <base-button @click="setSelectedTab('stored-resources')" :mode="storedRestButtonMode"
      >Stored Resources</base-button
    >
    <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode"
      >Add Resources</base-button
    >
  </base-card>
  <component :is="selectedTab"></component>
   <keep-alive></keep-alive>
  </div>
</template>


<script>
import StoredResources from './StoredRescouce.vue';
import AddResource from './AddRescources.vue'

export default {
  components:{
    StoredResources,
    AddResource
  },
  data() {
    return{
      selectedTab:'stored-resources',
      storedResources:[
        {id:'offiical-guid',
        title:'official Guide.;',
        description:'The offical Vue.js documentation.',
        link:'https://vuejs.org'
        },
         {id:'google',
        title:'Google;',
        description:'Learn to google...',
        link:'https://google.org'
        }
      ]
    }
   
  },
   provide(){
      return {
        resources: this.storedResources,
        addResource:this.addResource,
        deleteResource: this.removeResource
      };

    },
    computed:{
     storedRestButtonMode(){
      return this.selectedTab === 'stored-resources' ? null :'flat'
     },
     addResButtonMode(){
      return this.selectedTab === 'add-resources' ? null :'flat'
     }
    },
  methods:{
    setSelectedTab(tab){
      this.selectedTab = tab
    },
    addResource(title,description,url){
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link:url
      };
      this.storedResources.unshift(newResource);
      this.selectedTab='stored-resources'
      
    },
    removeResource(resId){
      const resIndex = this.storedResources.findIndex(res=>
      res.id === resId)
      this.storedResources.splice(resIndex,1)

    }
 }
}
</script>