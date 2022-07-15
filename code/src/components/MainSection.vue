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
                        <option 
                        v-for = "(city, index) in  cities" 
                        :key="index"
                        >{{city}}</option> 
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
    async fetchTransport() {
      const result = await fetch('http://localhost:3000/transport')
      this.transports = await result.json() 
      this.setCities(this.transports)
    },

    setCities(transports){
      const allCities = transports.map(function(element) {
        return element.city;
      });
      this.cities = [...new Set(allCities)] 
    },

    numbersOnly(evt) {
      evt = (evt) ? evt : window.event;
      var charCode = (evt.which) ? evt.which : evt.keyCode;
      if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
        evt.preventDefault();
      } else {
        return true;
      }
    },

    getTransportByCity(city){
      return this.transports.filter(transport => {
        return transport.city === city
      })
    },

    setCheaperShipping(items){
      const id = items[0].id
      this.cheaperShipping =  this.transports[id]
    },

    setFasterShipping(items){
      const id = items[0].id
      this.fasterShipping = this.transports[id]
    },

    getManipulateData(city){
      const destiny = JSON.parse(JSON.stringify(this.getTransportByCity(city))) 
      console.log('desteny', destiny);
      return destiny.map(function(item) {  
            item.lead_time = (item.cost_transport_heavy.split('h'))[0]; 
            item.cost_transport_heavy = (item.cost_transport_heavy.split(' '))[1]
            item.cost_transport_light = (item.cost_transport_light.split(' '))[1]
            return item; 
        })
    },

    analyze(){
       this.cheaperShipping = {}
       
       this.fasterShipping = {}
       const newItems = this.getManipulateData(this.city)

       let sortedItemsByCost = []
       let sortedItemsByTime = []

       if (this.weight > 100){
        sortedItemsByCost = newItems.sort((a, b) => a.cost_transport_light - b.cost_transport_light)
       }else{
        sortedItemsByCost = newItems.sort((a, b) => a.cost_transport_heavy - b.cost_transport_heavy)
       }
       
       sortedItemsByTime = newItems.sort((a, b) => a.lead_time - b.lead_time)
      
        this.setFasterShipping(sortedItemsByTime )
        this.setCheaperShipping(sortedItemsByCost )
       //console.log(sortedItemsByCost);
    }
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