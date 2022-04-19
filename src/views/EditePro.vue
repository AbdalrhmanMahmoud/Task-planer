<template>
<h1>Fuck you</h1>
  <form @submit.prevent="handleSubmit">
    <label> title:</label>
    <input v-model="title" type="text" required>

    <label>Details </label>
    <textarea  v-model="details" required></textarea>
    <div id="bt"> 
      <label > imoprtant </label>
<input v-model="important" type=checkbox  > 
    </div>
    <button>Update </button>
  </form>
</template>


<script>
export default {
  props:['id'],
  data(){
    return {
      title:" ",
      details:" ",
      important:false,
      uri:'http://localhost:3000/projects/' +this.id
    }
  },
  mounted() {
    fetch(this.uri)
    .then(res =>res.json())
    .then(data =>{
      // console.log(data)
      this.title = data.title
      this.details = data.details
      this.important = data.important

    })

  },
  methods:{
    handleSubmit(){
       fetch(this.uri,{
        method:'PATCH',
        headers:{'Content-Type': 'application/json'},
        body:JSON.stringify
        ({title: this.title ,
        details :this.details,
        important: this.important})
      }).then(() =>{
        this.$router.push('/')
      })
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