<template>
  <h1 class="text-dark">User Info</h1>
  <form class="col-md-3 mx-auto" v-if="showForm" @submit.prevent="handleSubmit">
    <label>First Name:</label>
    <input type="text" class="form-control p-1" v-model="firstName" required><br>

    <label>Last Name:</label>
    <input type="text" class="form-control" v-model="lastName" required><br>

    <label>Email:</label>
    <input type="email" class="form-control" v-model="email" required><br>

    <label>DOB:</label>
    <input type="date" class="form-control" v-model="dob" required><br>
    
    <label>Gender:</label>
    <select class="form-control" v-model="gendar" required>
      <option value="male">Male</option>
      <option value="female">Female</option>
      <option value="others">Others</option>
    </select><br>

    <div>
      <button  class="btn btn-dark">Submit</button>
    </div>
  </form>
   
   <div v-if="showTable"> 
     <table class="table">
       <tr v-for="index in list"  :key="index">
         
         <td>{{index.firstname}}</td>
         <td>{{index.lastname}}</td>
         <td>{{index.dob}}</td>
         <td>{{index.email}}</td>
         <td>{{index.gendar}}</td>
         <button class="btn btn-dark" @click="edit(index)">Edit</button>
         <button class="btn btn-dark" @click="assign(index)">Delete</button>
         <div class="yesbtn" v-if="index.showdelete">
           <label>Are you sure want to delete?</label>
           <button class="btn btn-dark" @click="deleteYes(index)">Yes</button>
           <button class="btn btn-dark" @click="deleteNo(index)">No</button>
         </div>
       </tr>
     </table>
   </div>

    <button class="btn btn-dark add"  @click="addItem">Add Item</button>
    
</template>

<script>


export default {
  name: 'App',
  components: { },
  data(){
    return{
      firstName:'',
      lastName: '',
      email: '',
      dob:'',
      gendar:'',
      id: 0,
      list:[],
      showTable: false,
      showForm: false,
      showDelete:false,
      editStatus: false,
      editItem: null,
    }
   },
   methods: {
     handleSubmit(){
       if(this.editStatus){
         
         this.list.forEach(
           (item)=>{
             if(this.editItem.id===item.id){
               console.log("match");
               this.editItem.firstname=this.firstName;
               console.log(this.editItem.firstname);
               this.editItem.lastname=this.lastName;
               this.editItem.dob=this.dob;
               this.editItem.email=this.email;
               this.editItem.gendar=this.gendar;
               console.log(this.editItem);
             }
             if(this.list.includes(this.editItem)){
               console.log('yes includes')
             }
             
           }
         );
         console.log(this.list);
         
       }
       else{
         const obj={
         firstname:this.firstName,
         lastname:this.lastName,
         dob:this.dob,
         email:this.email,
         gendar:this.gendar,
         id:this.id,
         showdelete: this.showDelete,
       }
       this.id++;
       console.log("submit",obj);
      
       
      
       
       
      
       this.list.push(obj);
       this.showTable=true;
       this.showForm=false
       };
       this.firstName='';
       this.lastName='';
       this.dob='';
       this.email='';
       this.gendar='';
      this.showTable=true;
       this.showForm=false;
       this.editItem=null;
       this.editStatus=false;
       },
    
     addItem(){
       
       this.showTable= false;
       this.showForm= true;
       
     },
     edit(index){
       this.editItem=index;
       this.editStatus=true;
       this.firstName= this.editItem.firstname;
       
       this.lastName=this.editItem.lastname;
       this.dob=this.editItem.dob;
       this.email=this.editItem.email;
       this.gendar=this.editItem.gendar;
       this.id=this.editItem.id;
       this.showForm=true;
       

      //  this.list[this.id].firstname=this.firstName;
      //  this.list[this.id].lastname=this.lastName;
      //  this.list[this.id].dob=this.dob;
      //  this.list[this.id].email=this.email;
      // //  this.list[this.id].id=this.id;
      //  this.list[this.id].gendar=this.gendar;

      //  index=this.list[this.id];
      
      //  console.log(this.list[this.id]);
      //  this.list[this.id]=''
      
      // this.deleteYes(this.list[this.id]);

     },
     assign(index){
         
        console.log(index.id);
        index.showdelete=true
               
     },
     deleteYes(index){
       const itemToDelete=index;
       this.list=this.list.filter(item=> item!== itemToDelete );
       this.showDelete=false;
     },
     deleteNo(index){
       index.showdelete=false;
     }

   }
}


</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}
.add{
  position: absolute;
  bottom: 30px;
  right: 600px;
}
table,tr,td{
  margin: 10px;

}
.yesbtn{
  background-color: lightblue;
  position: absolute;
  top: 150px;
  right: 100px;
}

</style>
