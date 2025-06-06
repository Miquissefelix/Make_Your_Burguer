<template>
  <div>
   <Message :msg="msg" v-show="msg"/>
    <div>
        <form id="burguer-form" @submit="createBurguer($event)">
          <div class="input-container">
            <label for="name">Nome do cliente:</label>
            <input type="text" id="name" name="name" placeholder="Digite o seu nome" required>
          </div>

           <div class="input-container">
            <label for="pao">Escolha o pao:</label>
             <select name="pao" id="pao" v-model="pao">
                <option value="">selecione o seu pao</option>
                <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
             </select>
          </div>

          <div class="input-container">
            <label for="carne">Escolha a carne do seu burguer:</label>
             <select name="carne" id="carne" v-model="carne">
                <option value="">selecione a sua carne</option>
                <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
             </select>
          </div>

          
          <div id="opcionais-container" class="input-container">
            <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
            <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
              <input type="checkbox" id="opcionais" name="opcionais" v-model="opcionais" :value="opcional.tipo"/>
             <span>{{ opcional.tipo }}</span>
            </div>
          </div>

          <div class="input-container">
             <input type="submit" class="submit-btn" value="Criar meu burguer" />
          </div>

        </form>
    </div>
  </div>
</template>

<script>
import Message from './Message.vue';
export default {
name: 'BurguerForm',
components: {
    Message
},
data(){
    return {
        //dados iniciais do json
        paes:null,
        carnes:null,
        opcionaisdata:null,
        nome:null,

        pao:null,
        carne:null,
        opcionais: [],
        msg:null
    }
},
methods:{
   async getIgredientes(){
    const req =await fetch("http://localhost:3000/ingredientes");
    const data=await req.json();
    this.paes = data.paes;
    this.carnes = data.carnes;
    this.opcionaisdata = data.opcionais;
   
    
   },

   async createBurguer(e){
    e.preventDefault();

    const data = {
        nome: e.target.name.value,
        pao: this.pao,
        carne: this.carne,
        opcionais:Array.from(this.opcionais) ,
        status:"Solicitado",
    };
    const dataJson = JSON.stringify(data);

    const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: {"Content-Type": "application/json"},
        body: dataJson
    });

    const res = await req.json();

    //sucess message
    this.msg =`Pedido realizado com sucesso!`;

    //clean message after 3 seconds
    setTimeout(()=>{
        this.msg = "";
    },3000)
  
    //clean form
    this.pao=""; 
    this.carne="";
    this.opcionais = "";
    this.nome = "";

    
   }
},
mounted(){
    this.getIgredientes();
}
}
</script>

<style scoped>
#burguer-form{
    max-width: 400px;
    margin: 0 auto;
}
.input-container{
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label{
    font-weight: bold;
    margin-bottom: 10px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
}
input, select{
    padding:5px 10px;
    width: 300px;
}
#opcionais-container{
    flex-direction: row;
    flex-wrap: wrap;
}
#opcionais-title{
   width: 100%;
}
.checkbox-container{
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}
.checkbox-container span,
.checkbox-container input{
 width: auto;
}
.checkbox-container span{
    margin-left: 6px;
    font-weight: bold;
}
.submit-btn {
background-color: #222;
  color: #fcba03;
  
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    font-weight: bold;
    transition: .5s;
}
.submit-btn:hover {
    background-color: transparent;
    color: #222;
 
}
</style>