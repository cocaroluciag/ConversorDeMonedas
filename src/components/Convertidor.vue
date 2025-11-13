<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <div class="container pt-3">
      <div class="row">
        <div class="col-lg-12">
          <div class="form-group">
            <label for="cantidad">Ingrese Cantidad</label>
            <input
              type="number"
              class="form-control form-control-lg"
              id="cantidad"
              placeholder="Ingrese cantidad.."
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
              <option v-for="(moneda, index) in monedas" :key="index">
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
              <option v-for="(moneda, index) in monedas" :key="index">
                {{ moneda }}
              </option>
            </select>
          </div>
        </div>
      </div>

      <div class="text-center pt-4">
        <h5 v-if="cantidad > 0">
          <span class="badge badge-success">{{ cantidad }} {{ tengo }}</span>
          <span class="badge badge-dark"> SON </span>
          <span class="badge badge-success">{{ getTotal(total) }} {{ quiero }}</span>
        </h5>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppConvertidor',
  data() {
    return {
      monedas: ["USD", "EUR", "LIBRA", "ARS"], // 💰 Agregamos pesos argentinos
      cantidad: 0,
      tengo: "USD",
      quiero: "EUR",
      total: 0,
    };
  },
  methods: {
    onChange() {
      switch (this.tengo) {
        // USD
        case "USD":
          if (this.quiero === "USD") this.total = this.cantidad;
          if (this.quiero === "EUR") this.total = this.cantidad * 0.84;
          if (this.quiero === "LIBRA") this.total = this.cantidad * 0.75;
          if (this.quiero === "ARS") this.total = this.cantidad * 1000;
          break;

        // EUR
        case "EUR":
          if (this.quiero === "USD") this.total = this.cantidad * 1.19;
          if (this.quiero === "EUR") this.total = this.cantidad;
          if (this.quiero === "LIBRA") this.total = this.cantidad * 0.89;
          if (this.quiero === "ARS") this.total = this.cantidad * 1190;
          break;

        // LIBRA
        case "LIBRA":
          if (this.quiero === "USD") this.total = this.cantidad * 1.33;
          if (this.quiero === "EUR") this.total = this.cantidad * 1.12;
          if (this.quiero === "LIBRA") this.total = this.cantidad;
          if (this.quiero === "ARS") this.total = this.cantidad * 1330;
          break;

        // ARS
        case "ARS":
          if (this.quiero === "USD") this.total = this.cantidad / 1000;
          if (this.quiero === "EUR") this.total = this.cantidad / 1190;
          if (this.quiero === "LIBRA") this.total = this.cantidad / 1330;
          if (this.quiero === "ARS") this.total = this.cantidad;
          break;
      }
    },
    getTotal(valor) {
      return Math.round(valor * 100) / 100;
    },
  },
};
</script>

<style scoped>
.container {
  max-width: 600px;
  margin-top: 30px;
  background-color: #1e1e1e; /* 🌑 Fondo oscuro */
  border-radius: 10px;
  padding: 25px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
}

label {
  font-weight: 700;
  font-size: 130%;
  color: white; /* 🤍 Texto de las etiquetas en blanco */
}

.form-control {
  background-color: #2c2c2c; /* Campos más oscuros */
  color: white;
  border: 1px solid #444;
}

.form-control:focus {
  border-color: #00b894; /* Verde brillante al seleccionar */
  box-shadow: 0 0 5px #00b894;
}

.badge {
  margin: 2px;
  font-size: 150%;
}
</style>