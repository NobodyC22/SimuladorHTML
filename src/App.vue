<template>
  <div class="content">
    <h1>GENERADOR DE APUESTAS</h1>
    <form v-on:submit.prevent="generar(op)">
      <select id="cant" v-model="op" :disabled="comprobar()">
        <option disabled value="">Please select one</option>
        <option value="1">1</option>
        <option value="2">2</option>
        <option value="3">3</option>
        <option value="4">4</option>
        <option value="5">5</option>
        <option value="6">6</option>
        <option value="7">7</option>
        <option value="8">8</option>
        <option value="9">9</option>
        <option value="10">10</option>
      </select>
      <br />
      <input type="submit" value="generar apuestas" :disabled="comprobar()" />
    </form>
    <form>
      <input type="radio" id="reint" value="Reintegro" v-model="test" :disabled="comprobar()"/>
      <label for="reint">Reintegro</label>
      <br />
      <input type="radio" id="three" value="3" v-model="test" :disabled="comprobar()"/>
      <label for="three">3 aciertos</label>
      <br />
      <input type="radio" id="four" value="4" v-model="test" :disabled="comprobar()"/>
      <label for="four">4 aciertos</label>
      <br />
      <input type="radio" id="five" value="5" v-model="test" :disabled="comprobar()"/>
      <label for="five">5 aciertos</label>
      <br />
      <input type="radio" id="five+" value="5+" v-model="test" :disabled="comprobar()"/>
      <label for="five+">5 aciertos + complementario</label>
      <br />
      <input type="radio" id="six" value="6" v-model="test" :disabled="comprobar()"/>
      <label for="six">6 aciertos</label>
      <br />
      <input type="radio" id="six+" value="6+" v-model="test" :disabled="comprobar()"/>
      <label for="six+">6 aciertos + reintegro</label>
      <br />
    </form>
    <table border="1">
      <tr>
        <td>Apuesta</td>
        <td>Num.1</td>
        <td>Num.2</td>
        <td>Num.3</td>
        <td>Num.4</td>
        <td>Num.5</td>
        <td>Num.6</td>
        <td>Compl.</td>
        <td>Reint.</td>
      </tr>

      <tr v-for="(apuesta, key) in apuestas" :key="apuesta">
        <td>{{ key + 1 }}</td>
        <td>{{ apuesta.num_1 }}</td>
        <td>{{ apuesta.num_2 }}</td>
        <td>{{ apuesta.num_3 }}</td>
        <td>{{ apuesta.num_4 }}</td>
        <td>{{ apuesta.num_5 }}</td>
        <td>{{ apuesta.num_6 }}</td>
        <td class="comple">{{ apuesta.comple }}</td>
        <td class="reint">{{ apuesta.reint }}</td>
      </tr>
    </table>
    <button @click="simular()">SIMULAR</button>
  </div>
</template>

<script>
export default {
  data: () => ({
    key: "",
    num_1: "",
    num_2: "",
    num_3: "",
    num_4: "",
    num_5: "",
    num_6: "",
    comple: "",
    reint: "",
    apuestas: [],
    cartillasSemanales: [],
    test: "",
    op: 0,
  }),
  methods: {
    generar(cantidad = 1) {
      for (let i = 0; i < cantidad; i++) {
        let preapuesta = [];

        for (let i = 0; i < 7; i++) {
          let posiblenum = Math.floor(Math.random() * (50 - 1)) + 1;
          if (i >= 1) {
            for (let j = 0; j < i; j++) {
              if (preapuesta[j] == posiblenum) {
                i = 0;
                break;
              }
            }
          }
          preapuesta[i] = posiblenum;
        }
        preapuesta[7] = Math.floor(Math.random() * (10 - 1)) + 1;
        this.apuestas.push({
          num_1: preapuesta[0],
          num_2: preapuesta[1],
          num_3: preapuesta[2],
          num_4: preapuesta[3],
          num_5: preapuesta[4],
          num_6: preapuesta[5],
          comple: preapuesta[6],
          reint: preapuesta[7],
        });
      }
    },
    comprobar() {
      if(this.apuestas.length>0) {
        return true;
      }
      return false;
    },
    simular(cantidad = 2) {
      for (let i = 0; i < cantidad; i++) {
        let preapuesta = [];

        for (let i = 0; i < 7; i++) {
          let posiblenum = Math.floor(Math.random() * (50 - 1)) + 1;
          if (i >= 1) {
            for (let j = 0; j < i; j++) {
              if (preapuesta[j] == posiblenum) {
                i = 0;
                break;
              }
            }
          }
          preapuesta[i] = posiblenum;
        }
        preapuesta[7] = Math.floor(Math.random() * (10 - 1)) + 1;
        this.cartillasSemanales.push({
          num_1: preapuesta[0],
          num_2: preapuesta[1],
          num_3: preapuesta[2],
          num_4: preapuesta[3],
          num_5: preapuesta[4],
          num_6: preapuesta[5],
          comple: preapuesta[6],
          reint: preapuesta[7],
        });
      }
    }
  },
};
</script>

<style>
.reint {
  background-color: rgb(90, 90, 235);
}
.comple {
  background-color: rgb(253, 153, 114);
}
</style>