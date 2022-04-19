<template>
  <div class="project" :class="{complete :p.complete}">
      <div class="actions">
        <h3 @click="toggleDetails =!toggleDetails">{{p.title}}</h3> 
        <div class="io">
          <router-link :to="{name:'EditePro', params:{id:p.id}}">
            <span class="material-icons edit">edit</span>
          </router-link>
        <span @click="deleteT" class="material-icons red">delete</span>
        <span @click="toggleComplete"  class="material-icons done">done</span>
        <span @click="toggleImortant" :class="{importantx :p.important}" class="material-icons">grade</span>

        </div>

      </div>
      <div  v-if="toggleDetails" class="details ">
       {{ p.details }}
      </div>

  </div>
</template>

<script>
export default {
  props: ["p"],
  data() {
    return {
      toggleDetails:false,
      uri:'http://localhost:3000/projects/' +this.p.id
    }
  },
  methods: {
    deleteT(){
      fetch(this.uri,{method:'Delete'})
      .then(() => this.$emit('delete',this.p.id))
      .catch(err => console.log(err.massage))

    },
    toggleComplete(){
      fetch(this.uri,{
        method:'PATCH',
        headers:{'content-type':'application/json'},
        body:JSON.stringify({complete: !this.p.complete})
      }).then(() => {
        this.$emit('complete',this.p.id)
      })
    },
    toggleImortant(){
      fetch(this.uri,{
        method:'PATCH',
        headers:{'content-type':'application/json'},
        body:JSON.stringify({important: !this.p.important})
      }).then(() => {
        this.$emit('important',this.p.id)
      })
    }











    ////
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.project{
  margin: 20px auto;
  background: #fff;
  padding: 10px 20px ;
  border-radius: 5px;
  box-shadow: 1px 2px 3px rgba(0,0,0,0.5);
  border-left: 4px solid#ff3414;
  .actions{
    display: flex;
    justify-content: space-between;
    align-items: center;
  h3{
    cursor: pointer;
  }
  .io{
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
  span{
        &:hover{
      color: #000;
      
    }
  }
  }

  }

}
#gold{
  color: gold;
}
.project.complete{
    border-left: 4px solid #42b983;

}
.project.complete .done{
  color: #42b983;
  font-size: 1.1em;
  font-weight: bold;
}
// .project span

.importantx{
  color: gold;
}
.red:hover{
color: #f00 !important
}
.edit{
  color: #ddd;

&:hover{
    color: #42b983 !important
  }
}
</style>
