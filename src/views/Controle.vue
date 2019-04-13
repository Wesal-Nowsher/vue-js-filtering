<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
  <div id="app">
    <v-app id="inspire">
      <div v-if="data">
        <v-card-title>
          Contrôles
          <v-spacer></v-spacer>
          <v-text-field
            v-model="search"
            append-icon="search"
            label="Search"
            single-line
            hide-details
          ></v-text-field>
        </v-card-title>
        <v-data-table :search="search" :headers="headers" :items="data" class="elevation-1">
          <template v-slot:items="props">
            <td   v-for="(item, key) in headers" :key="key"><p v-bind:class='{ "redcolor": props.item["blue"]==="red"}'>{{props.item["error"]}} {{ props.item[item.value] }}</p></td>
          </template>
        </v-data-table>
      </div>
      <div v-else>
        data not found go to
        <router-link to="/importation">importation</router-link>and import for see data
      </div>
    </v-app>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: ""
    };
  },
  methods:{
          getUnits: function() {
          console.log("wesal is mkaig this onb apge load");
          console.log(this.data);
          }
      },
  created: function(){
         this.getUnits()
       },
  computed: {
    data() {
        var self=this;
        var index=0;
        while(index  < self.$store.state.data.length -4){
         console.log("index",index);
            if(index < self.$store.state.data.length -4){

            if(parseInt(self.$store.state.data[index]["Cotes Dernière"].replace(",",".")) < parseInt(self.$store.state.data[index+3]["Cotes Dernière"].replace(",","."))){
                                console.log("goora che 13 razi" ,index,self.$store.state.data[index+3]["Cotes Dernière"].replace(",","."));
                                self.$store.state.data[index+3]["blue"]= "red";
                        }
                        else{
                            self.$store.state.data[index+4]["blue"]= "black";
                        }
            }

            index=index+3;
            console.log(index);
        }

       var indexi=2;
            while(indexi  < self.$store.state.data.length -4){
             console.log("index",indexi);
                if(indexi < self.$store.state.data.length -4){
                if(parseInt(self.$store.state.data[indexi]["Cotes Dernière"].replace(",",".")) > parseInt(self.$store.state.data[indexi+3]["Cotes Dernière"].replace(",","."))){
                                    console.log("goora che 13 razi" ,indexi,self.$store.state.data[indexi+3]["Cotes Dernière"].replace(",","."));
                                    self.$store.state.data[indexi+3]["blue"]= "red";
                            }
                            else{
                                self.$store.state.data[indexi+4]["blue"]= "black";
                            }
                }

                indexi=indexi+3;
                console.log(index);
            }
      return this.$store.state.data;
    },
    headers() {
        console.log("kam",this.data[0])
      return Object.keys(this.data[0])
        .slice(0, 11)
        .map(k => ({
          text: k,
          value: k,
          width: "1%",
        }));
    },
  }
};
</script>

<style scoped>
table.v-table tbody td:first-child, table.v-table tbody td:not(:first-child), 
table.v-table tbody th:first-child, table.v-table tbody th:not(:first-child), 
table.v-table thead td:first-child, table.v-table thead td:not(:first-child), 
table.v-table thead th:first-child, table.v-table thead th:not(:first-child) {
  padding: 0 10px !important;
  width: 1%
}
.redcolor{
    color:red;
}
</style>

