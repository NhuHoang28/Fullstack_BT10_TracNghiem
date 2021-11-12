<template>
  <div id="app">   
    <div v-for="(cauHoi,index) in boCauHoi" :key="index" class="title">
      <a href="#" @click.prevent="show=cauHoi.cau-1" :class="{chon:show==cauHoi.cau-1}"> cau hoi {{cauHoi.cau}}</a>
    </div>
    <br>
    <div class="main">
      {{boCauHoi[show].cauHoi}}
      <div v-for="(dapan,index) in boCauHoi[show].dapAn" :key="index">
        <input type="radio" :value="dapan" v-model="boCauHoi[show].chon"> {{dapan}} 
      </div> 
    </div>
    <div class="change">  
      <button @click="show--">back</button>
      <button @click="show++">next</button> 
      <button @click="nopbai()">nopbai</button>  
    </div>
     <div v-show="submiting">
       <table>
         <tr>
           <th>cau hoi so</th>
           <th> cau hoi</th> 
           <th> dap an dung</th> 
           <th> ban chon</th> 
           <th> diem cho cau nay</th> 
         </tr>
         <tr v-for="(cau,index) in boCauHoi" :key="index" >
           <td>{{cau.cau}}</td>
           <td>{{cau.cauHoi}}</td>
           <td>{{cau.dapAnDung}}</td>
           <td>{{cau.chon}}</td>
           <td>{{cau.diem}}</td>
         </tr>
       </table> 
    ĐIỂM CỦA BẠN:  {{this.diem}} 
     </div>
  </div>
</template>

<script>    
export default {  
 data(){
   return {
     show:0,
     submiting:false,
     diem:0,
     boCauHoi:[
       {cau:1,cauHoi:"1+1=?",dapAn:['1','2','3','4'],dapAnDung:'2',diem:1,chon:''},
       {cau:2,cauHoi:"1+2=?",dapAn:['7','5','3','6'],dapAnDung:'3',diem:1,chon:''},
       {cau:3,cauHoi:"1+3=?",dapAn:['9','22','32','4'],dapAnDung:'4',diem:0.5,chon:''}
     ]
   }
 },
 watch:{
   show(){
     if(this.show<0)
     this.show=0;  
     else if(this.show>this.boCauHoi.length-1)
     this.show=this.boCauHoi.length-1;
   }
 },
 methods:{
   nopbai(){
     this.submiting=true;
     this.diem=0;
     this.boCauHoi.filter(cauhoi=>{
     return cauhoi.dapAnDung==cauhoi.chon
    })
    .forEach( cauhoi =>{
       this.diem+=cauhoi.diem ;
    },0);
     
   }
 }
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale; 
}
 table{
   margin:10px;
 }
th ,td{ 
  padding:4px;
  margin:0px;  
  background-color:rgba(0,0,0,0.2);
}
#app .title{
  display: inline-block; 
  border:1px solid black;
  margin:2px;
  border-radius:3px;
}
a{
  text-decoration: none;
  color:black;
  padding:0px 10px;
}
.chon{
  background-color:rgba(0,0,0,0.4);

}
.main{
  padding:10px; 
  margin:20px 10px;
  background-color: rgba(0,0,0,0.1); 
}
button{
  margin: 5px;
}
</style>
