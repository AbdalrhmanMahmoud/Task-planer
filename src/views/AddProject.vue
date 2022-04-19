<template>
  <form @submit.prevent="handleSubmit">
    <label> title:</label>
    <input v-model="title" type="text" required>

    <label>Details </label>
    <textarea  v-model="details" required></textarea>
    
    <div id="bt"> 
      <label > imoprtant </label>
<input v-model="important" type=checkbox  > 
    </div>

    <button>Add </button>
  </form>
</template>


<script>
export default {
  data(){
    return {
      title:" ",
      details:" ",
      important:false
      
    }
  },
  methods:{
    handleSubmit(){
      let newProject ={
        title: this.title,
        details: this.details,
        complete :false,
        important :this.important
      }
      fetch('http://localhost:3000/projects',{
        method:'POST',
        headers:{'Content-Type': 'application/json'},
        body:JSON.stringify(newProject)
      }).then(() =>{
        this.$router.push('/')
      })
      console.log(newProject)
    }
  }




}
</script>

<style lang="scss" scoped>
*{
    box-sizing: border-box;

}
form{
  background: #fff;
  padding: 20px;
  border-radius: 10px;
  label{
    display: block;
    color:#a9a;
    font-size: 15;
    font-weight: bold;
    margin: 20px 0 10px 0;
  }
  input{
    padding: 10px;
    border:0;
    color: #000;
    border-bottom: 1px solid #ddd;
    width:100%;
  }
  textarea{
    border: 1px solid #ddd;
    padding: 10px ;
    width :100%;
    height: 100px;
  }
  button{
    display: block;
    margin:20px auto 0;
    background: #00ce89;
    color: #fff;
    padding: 10px;
    border: 0;
    border-radius: 7px;
    font-size: 17px;
  }
}
#bt{
  height: 70px;
  padding-top: 20px;
  label,
  input{
    display: inline;
    width: 50%;
    margin-left: 20px;
    color: #000 ;
    letter-spacing: .1px;
    font-size: 1.2em;
  }
  input{
    height: 17px;

  }

}
</style>