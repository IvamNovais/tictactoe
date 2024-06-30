<template>
  <div class="pagina">
    <div class="tabuleiro">
      <div class="linha" v-for="(linha, index) in tabuleiro" :key="index">
        <div class="casa" v-for="(casa, indexCasa) in linha" :key="indexCasa">
          <button class="botao_casa" :class="casa" @click="marca(index, indexCasa)">{{ casa }}</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: 'HomeView',
  components: {
  },
  data() {
    return {
      tabuleiro: this.criaTabuleiro(),
      vezDe: "X",
      linhas:[0,0,0],
      colunas:[0,0,0],
      diagonais:[0,0]
    }
  },
  created() {
  },
  methods: {
    criaTabuleiro() {
      let matrix = [];
      for (let i = 0; i < 3; i++) {
        matrix[i] = [];
        for (let j = 0; j < 3; j++) {
          matrix[i][j] = "";
        }
      }
      return matrix;

    },
    marca(x, y) {
      if (this.tabuleiro[x][y] === "") {
        this.$set(this.tabuleiro[x], y, this.vezDe)
        if(this.checkWin(x,y)){
          window.alert("vitoria de "+ this.vezDe)
          this.reset()
        }
        this.vezDe = this.vezDe === "X" ? "O" : "X";
      }
    },
    checkWin (x,y) {
      this.linhas[x] = this.vezDe==="X"? this.linhas[x]+1:this.linhas[x]-1
      this.colunas[y] = this.vezDe==="X"? this.colunas[y]+1:this.colunas[y]-1

      if(x===y){
        this.diagonais[0] = this.vezDe==="X"? this.diagonais[0]+1:this.diagonais[0]-1
        if(this.diagonais[0]===3||this.diagonais[0]===-3){
          return true
        }
      }
      return this.linhas[x]===3||this.linhas[x]===-3||this.colunas[y]===3||this.colunas[y]===-3

    },
    reset(){
      this.$set(this.tabuleiro, this.criaTabuleiro)
      this.linhas = [0,0,0]
      this.colunas=[0,0,0]
      this.diagonais=[0,0]
    }
  }
}
</script>
<style>
* {
  margin: 0;
  padding: 0;
}

.pagina {
  display: grid;
  grid-template-columns: 500px;
  justify-content: center;
  align-content: center;
  height: 100vh;

}

.tabuleiro {
  border: 1px black solid;
  height: 500px;
  width: 500px;
}

.linha {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  height: 33.3%;
}

.casa {
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px black solid;
}

.botao_casa {
  border: none;
  height: 100%;
  width: 100%;
  cursor: pointer;
}

.X {
  font-size: 100px;
  color: red;
  font-weight: bold;
}
.O {
  font-size: 100px;
  color: blue;
  font-weight: bold;
}
</style>
