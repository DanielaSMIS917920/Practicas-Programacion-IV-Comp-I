 <template>
  <div>
    <div class="container pt-3">
      <h1>CONVERSOR DE MONEDAS</h1>
      <div class="row">
        <div class="col-lg-12">
          <div class="form-group">
            <label for="cantidad">Ingrese Cantidad</label>
            <input
              type="number"
              class="form-control form-control-lg"
              id="cantidad"
              placeholder="Ingrese cantidad"
              v-model="cantidad"
              v-on:keyup="onChange"
            />
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-lg-6">
          <div class="form-group">
            <label for="tengo">Tengo</label>
            <select
              class="form-control form-control-lg"
              id="tengo"
              v-model="tengo"
              v-on:change="onChange()"
            >
              <option v-for="(moneda, index) in monedas" v-bind:key="index">
                {{ moneda }}
              </option>
            </select>
          </div>
        </div>
        <div class="col-lg-6">
          <div class="form-group">
            <label for="quiero">Quiero</label>
            <select
              class="form-control form-control-lg"
              id="quiero"
              v-model="quiero"
              v-on:change="onChange()"
            >
              <option v-for="(moneda, index) in monedas" v-bind:key="index">
                {{ moneda }}
              </option>
            </select>
          </div>
        </div>
      </div>
      <div class="text-center pt-4">
        <h5 v-if="cantidad > 0">
          <spam>{{ cantidad }} {{ tengo }}</spam>
          <spam > SON </spam>
          <spam>{{ getTotal(total) }} {{ quiero }}</spam>
        </h5>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      monedas: ["USD", "EUR", "LIBRA"],
      cantidad: 0,
      tengo: "USD",
      quiero: "EUR",
      total: 0,
    };
  },
  methods: {
    onChange() {
      switch (this.tengo) {
      
        case "USD":
          if (this.quiero === "USD") {
            this.total = this.cantidad;
          }
          if (this.quiero === "EUR") {
            this.total = this.cantidad * 0.84;
          }
          if (this.quiero === "LIBRA") {
            this.total = this.cantidad * 0.75;
          }
          break;
       
        case "EUR":
          if (this.quiero === "USD") {
            this.total = this.cantidad * 1.19;
          }
          if (this.quiero === "EUR") {
            this.total = this.cantidad;
          }
          if (this.quiero === "LIBRA") {
            this.total = this.cantidad * 0.89;
          }
          break;
        
        case "LIBRA":
          if (this.quiero === "USD") {
            this.total = this.cantidad * 1.33;
          }
          if (this.quiero === "EUR") {
            this.total = this.cantidad * 1.12;
          }
          if (this.quiero === "LIBRA") {
            this.total = this.cantidad;
          }
          break;
        default:
      }
    },
    getTotal(valor) {
        return Math.round(valor)
    }
  },
};
</script>

<style scoped>
.badge {
  margin: 2px;
  font-size: 150%;
}
label {
  font-weight: 700;
  font-size: 130%;
}
</style>
