<template>
  <div class="main-section">
    <div class="container">
        <div>
            <h3>Como é o frete que você precisa?</h3>
        </div>
        <div>
            <div>
                <div>
                    <label>
                        Destino
                    </label>
                </div>
                <div>
                    <select >
                        <option selected disabled value="">Select language</option> 
                    </select>
                </div>
            </div>
            <div>
                <div>
                    <label>
                        Peso
                    </label>
                </div>
                <div>
                    <input 
                        type="text" 
                        label="insira aqui o peso da carga em kg"
                    />
                </div>
            </div>
            <div>
                 <button type="button" >Analisar</button>
            </div>
        </div>
        <div>
            <h3>Essas são as melhores alternativas de frete que encontramos para  você</h3>
        </div>
        <div>
            <p>
            Frete mais Barato
            <span> Transportadora XYZ LTDA - R$ 500,00 - 12h</span>
            </p>
        </div>
        <div>
            <p>
            Frete mais Barato
            <span> Transportadora XYZ LTDA - R$ 500,00 - 12h</span>
            </p>
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
</style>