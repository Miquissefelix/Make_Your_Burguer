<template>
  <div>
    <p>component d messagem</p>
    <div>
        <form id="burguer-form">
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
              <input type="checkbox" id="Salame" name="opcionais" v-model="opcionais" :value="opcional.tipo"/>
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
export default {
name: 'BurguerForm',

data(){
    return {
        //dados iniciais do json
        paes:null,
        carnes:null,
        opcionaisdata:null,
        nome:null,

        pao:null,
        carne:null,
        opcional: [],
        status:"Solicitado",
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
    console.log(this.carnes);
    
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