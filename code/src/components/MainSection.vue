<template>
  <div class="main-section">
    <div class="container">
        <div class="header-container">
            <span>Como é o frete que você precisa?</span>
        </div>
        <div class = "form">
            <div class="destiny">
                <div>
                    <label>
                        Destino
                    </label>
                </div>
                <div id = "div-select">
                    <select >
                        <option selected disabled value="">Seleciona o destino do frete</option> 
                    </select>
                </div>
            </div>
            <div class="weight">
                <div>
                    <label>
                        Peso
                    </label>
                </div>
                <div id="div-input">
                    <input 
                        type="text" 
                        label="insira aqui o peso da carga em kg"
                    />
                </div>
            </div>
            <div class="container-submit">
                 <button type="button" >Analisar</button>
            </div>
        </div>
        <div class="result-tiltle">
            <span>Essas são as melhores alternativas de frete que encontramos para  você</span>
        </div>
        <div id="cheaperShipping">
            <span>Frete mais barato: <b>Transportadora XYZ LTDA - R$ 500,00 - 12h</b></span>
        </div>
        <div id="fasterShipping">
            <span>Frete mais rapido: <b>Transportadora XYZ LTDA - R$ 500,00 - 12h</b></span>  
        </div>
    </div>
  </div>

</template>

<script>

export default {
 data() {
    const appName = ''

    return {
      appName,
      transports:[],
      cities:[],
      weight:null,
      city:'',
      cheaperShipping: {},
      fasterShipping: {}
    }
  },
  created() {
    // Implemente aqui o GET dos dados da API REST
    // para que isso ocorra na inicialização da pagina
    this.fetchTransport()
  },
  methods: {
    // Implemente aqui os metodos utilizados na pagina
   
  }
}
</script>

<style scoped>
.main-section{
    display: flex;
    align-items: center;
    justify-content: center;
}

.main-section .container{
    max-width: 700px;
    padding:40px;
}

.main-section .container .header-container{
     border-bottom: 1px solid #000;
     max-width:400px;
     padding-left:10px;
     padding-right:10px;
     padding-bottom:5px;
}
.main-section .container .header-container span{
     font-size:1.25em;
     font-weight:bold;
}

.main-section .container .form{
    padding:30px;
}
.main-section .container .form .destiny{
    margin-bottom:30px;
}

.main-section .container .form .destiny > div:nth-of-type(1){
    margin-bottom:5px;
    font-size: 1.1em;
}

 #div-select{
     max-width:450px;
    
}

 #div-select select{
     width:100%;
     height:30px;
     background-color: #C9DAF8; 
     border: 1px solid;
    
}

.main-section .container .form .weight{
    margin-bottom:30px;
}

.main-section .container .form .weight > div:nth-of-type(1){
    margin-bottom:5px;
    font-size: 1.1em;
}

#div-input{
    max-width:450px;
}

#div-input input{
     width:100%;
     height:30px; 
     background-color: #C9DAF8;  
     border: 1px solid;
}

.container-submit{
    max-width: 450px;   
    display: flex;
    align-items: center;
    justify-content: center;
}

.container-submit button{
   width: 120px;
   padding: 5px;
   border: solid 1px #D9EAD3;
   border-radius: 5px;
   background-color: #D9EAD3
   
}



.main-section .container .result-tiltle{
     border-bottom: 1px solid #000;
    max-width:400px;
     padding-left:10px;
     padding-right:10px;
     padding-bottom:5px;
}

.main-section .container .result-tiltle span{
     font-size:1.25em;
     font-weight:bold;
     line-height:1em
}

#cheaperShipping{
    
    display: flex;
    margin-top:30px;
    border: dashed 1px #00ACA6;
    padding:10px;
    border-radius: 5px;
    background-color: #D9EAD3;
}



#fasterShipping{
    
    display: flex;
    margin-top:30px;
    border: dashed 1px #798395;
    padding:10px;
    border-radius: 5px;
    background-color: #C9DAF8;
}

</style>