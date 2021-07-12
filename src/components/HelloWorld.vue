<template>
  <div class="container">
    <div class="gaussianFilter">
      <div class="theory">
        <div style="margin-bottom: 10px;"><h4>Filtro Gaussiano</h4>
          <p>Los valores del filtro se obtienen de evaluar la función Gaussian</p>
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 210 60" height="60" width="210" style="margin: auto;">
            <rect x="0" y="0" width="210" height="60" fill="#ccc" stroke="#fff"/>
            <g transform="translate(0,-15)">
              <text x="10" y="50" font-size="15" fill="black">G(x,y) =</text>
              <line  x1="70" y1="45" x2="100" y2="45" stroke="#000"></line>
              <text x="80" y="40" font-size="15" fill="black">1</text>
              <text x="70" y="60" font-size="15" fill="black">2πσ</text>
              <text x="96" y="54" font-size="10" fill="black">2</text>
              <text x="105" y="50" font-size="15" fill="black">exp</text>
              <text x="130" y="55" font-size="35" fill="black">(</text>
              <text x="136" y="50" font-size="20" fill="black">-</text>
              <line x1="145" y1="46" x2="200" y2="46" stroke="#000"></line>
              <text x="155" y="40" font-size="15" fill="black">x + y</text>
              <text x="162" y="35" font-size="10" fill="black">2</text>
              <text x="188" y="35" font-size="10" fill="black">2</text>
              <text x="157" y="60" font-size="15" fill="black">2σ</text>
              <text x="183" y="55" font-size="10" fill="black">2</text>
              <text x="200" y="55" font-size="35" fill="black">)</text>
            </g>
          </svg>
        </div>
        <div style="margin-top: -30px;">
          <h5>Detalles</h5>
          <p style="margin-top: -25px;">Despues de calcular los valores de la función gaussiana se debe normalizar.</p>
          <p style="margin-top: -15px;">Primero se suman los elementos resultado de la función Gaussiana.</p>
          <p style="margin-top: -15px;">La normalización del filtro se hace dividiendo cada elemento entre la suma de todos los elementos.</p>
        </div>        
      </div>
      <div class="implementation">
        <div> <strong>Presione calcular para mostrar los elementos normalizados del filtro</strong></div>
       
        <div class="filter">
          <div :class="item.clase" :style="item.style" v-for="(item, index) in items" :key="index" >{{ isNaN(gs[index]) ? ' ' : gs[index] }}</div>
        </div>
        <div>
          <div style="margin: 0 0 10px 0;">
            <button @click="sizeChange(-2)" style="margin-right: 10px;">size:  -2</button>
            <span style="border: 3px solid black; padding: 0 5px 0 5px;">{{ size }} x {{ size }}</span>
            <button @click="sizeChange(2)" style="margin-left: 10px;">size + 2</button>
          </div>
          <div style="margin: 0 0 10px 0;">
            <button @click="sigmaChange(-0.1)" style="margin-right: 10px;">σ - .1</button>
            <span style="border: 3px solid black; padding: 0 4px 0 4px;">σ = {{ sigma }}</span>
            <button @click="sigmaChange(0.1)" style="margin-left: 10px;">σ + .1</button>
          </div>
          <div>
            <button @click="gaussian()">Calculate</button>
          </div>
        </div>
        
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      size: 3,
      sigma: 5.5,
      x: [4, 3, 2, 1, 0, 1, 2, 3, 4],
      y: [4, 3, 2, 1, 0, 1, 2, 3, 4],
      gs: [ NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, 
           NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN,
           NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN,
           NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN,
           NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN,
           NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN,
           NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN,
           NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN, NaN,
           NaN],
      sum: 0,
      items: [{clase: "oneOne item"},
              {clase: "twoOne item"},
              {clase: "threeOne item"},
              {clase: "fourOne item"},
              {clase: "fiveOne item"},
              {clase: "sixOne item"},
              {clase: "sevenOne item"},
              {clase: "eigthOne item"},
              {clase: "nineOne item"},
              {clase: "oneTwo item"},
              {clase: "twoTwo item"},
              {clase: "threeTwo item"},
              {clase: "fourTwo item"},
              {clase: "fiveTwo item"},
              {clase: "sixTwo item"},
              {clase: "sevenTwo item"},
              {clase: "eigthTwo item"},
              {clase: "nineTwo item"},
              {clase: "oneThree item"},
              {clase: "twoThree item"},
              {clase: "threeThree item"},
              {clase: "fourThree item"},
              {clase: "fiveThree item"},
              {clase: "sixThree item"},
              {clase: "sevenThree item"},
              {clase: "eigthThree item"},
              {clase: "nineThree item"},
              {clase: "oneFour item"},
              {clase: "twoFour item"},
              {clase: "threeFour item"},
              {clase: "fourFour item"},
              {clase: "fiveFour item"},
              {clase: "sixFour item"},
              {clase: "sevenFour item"},
              {clase: "eigthFour item"},
              {clase: "nineFour item"},
              {clase: "oneFive item"},
              {clase: "twoFive item"},
              {clase: "threeFive item"},
              {clase: "fourFive item"},
              {clase: "fiveFive item"},
              {clase: "sixFive item"},
              {clase: "sevenFive item"},
              {clase: "eigthFive item"},
              {clase: "nineFive item"},
              {clase: "oneSix item"},
              {clase: "twoSix item"},
              {clase: "threeSix item"},
              {clase: "fourSix item"},
              {clase: "fiveSix item"},
              {clase: "sixSix item"},
              {clase: "sevenSix item"},
              {clase: "eigthSix item"},
              {clase: "nineSix item"},
              {clase: "oneSeven item"},
              {clase: "twoSeven item"},
              {clase: "threeSeven item"},
              {clase: "fourSeven item"},
              {clase: "fiveSeven item"},
              {clase: "sixSeven item"},
              {clase: "sevenSeven item"},
              {clase: "eigthSeven item"},
              {clase: "nineSeven item"},
              {clase: "oneEight item"},
              {clase: "twoEight item"},
              {clase: "threeEight item"},
              {clase: "fourEight item"},
              {clase: "fiveEight item"},
              {clase: "sixEight item"},
              {clase: "sevenEight item"},
              {clase: "eigthEight item"},
              {clase: "nineEight item"},
              {clase: "oneNine item"},
              {clase: "twoNine item"},
              {clase: "threeNine item"},
              {clase: "fourNine item"},
              {clase: "fiveNine item"},
              {clase: "sixNine item"},
              {clase: "sevenNine item"},
              {clase: "eigthNine item"},
              {clase: "nineNine item"}],
              
    }
  },
  methods: {
    gaussian() {
      var half = (this.x.length-1) / 2
      var start = half - ((this.size -1) / 2)
      var end = half + ((this.size -1) / 2) + 1

      for (let i =0; i<this.gs.length; i++){
          this.gs[i] = NaN
          this.items[i].style = "grid-column: `${i}`; grid-row: `${j}`; border: 0px solid blue;"
      }

      for (let i=start; i<end; i++) {
        for (var j=start; j<end; j++) {
          var gss = (1/ (2 * Math.PI * Math.pow(this.sigma, 2))) * Math.exp(-(Math.pow(this.x[i],2) + Math.pow(this.y[j],2))/ (2 * Math.pow(this.sigma, 2)))
          // var gss =  Math.exp(-(Math.pow(this.x[i],2) + Math.pow(this.y[j],2))/ (2 * Math.pow(this.sigma, 2)))

          // gss = Math.round(10000 * gss) / 10000
          if (gss != 0){
            this.gs[i + j * (this.x.length)] = gss
            this.items[i + j * (this.x.length)].style = "grid-column: `${i}`; grid-row: `${j}`; border: 1px solid blue; align-self: center; justify-items: center; width: 60px; height: 40px;"
          } else {
            this.gs[i + j * (this.x.length)] = NaN
          }
        }
      }
      this.sum = 0;
      for (let i =0; i<this.gs.length; i++){
        if (!isNaN(this.gs[i])){
          this.sum += this.gs[i]
        }
      }

      for (var i =0; i<this.gs.length; i++){
        if (!isNaN(this.gs[i])){
          // console.log('gs i: ', this.gs[i])
          this.gs[i] = Math.round(10000000 * this.gs[i] / this.sum) / 10000000
          // this.items[i].style += "height: 40px;"
          
        }
      }
    },
    sigmaChange(change) {
      this.sigma = Math.round(100 * (this.sigma + change)) / 100
    },
    sizeChange(change) {
      this.size = this.size + change
      if (this.size < 3){
        this.size = 3
      }
      if (this.size > 9){
        this.size = 9
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.filter {
  display: grid;
  grid-template-columns: repeat(9, 60px);
  grid-gap: 0px;
  grid-auto-rows: minmax(40px, 40px);
  align-items: end;
  justify-items: stretch;
  font-size: 10px;
}

.container {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  width: auto;
}

.gaussianFilter {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 50%;
}

.theory {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: auto;
}
.implementation {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: auto;
}

.item {
  justify-items: center;
}

</style>
