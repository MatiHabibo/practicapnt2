<template>
  <section class="src-components-formulario">
    <h1>Formulario de pagos</h1>

    <vue-form :state="formState" @submit.prevent="enviar()">
      <validate tag="div">
        <label for="nombre">Nombre</label>
        <input
          type="text"
          id="nombre"
          name="nombre"
          class="form-control"
          autocomplete="off"
          v-model.trim="formData.nombre"
          required
          :minlength="nombreMinLength"
        />

        <field-messages name="nombre" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido
          </div>
          <div slot="minlength" class="alert alert-danger mt-1">
            Este campo requiere como mínimo {{ nombreMinLength }} caracteres.
          </div>
        </field-messages>
      </validate>
      <br />

      <validate tag="div">
        <label for="documento">Nro de documento</label>
        <input
          type="number"
          id="documento"
          name="documento"
          class="form-control"
          autocomplete="off"
          v-model.trim="formData.documento"
          required
          :minlength="nombreMinLengthDoc"
          :maxlength="nombreMaxLengthDoc"
        />

        <field-messages name="documento" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido
          </div>
          <div slot="minlength" class="alert alert-danger mt-1">
            Este campo requiere como mínimo {{ nombreMinLengthDoc }} caracteres.
          </div>
          <div slot="maxlength" class="alert alert-danger mt-1">
            Este campo requiere como maximo {{ nombreMaxLengthDoc }} caracteres.
          </div>
        </field-messages>
      </validate>
      <br />
      <validate tag="div">
        <label for="monto">Monto a pagar</label>
        <input
          type="number"
          id="monto"
          name="monto"
          class="form-control"
          autocomplete="off"
          v-model.trim="formData.monto"
          required
          :min="minimoMonto"
        />

        <field-messages name="monto" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido
          </div>
          <div slot="min" class="alert alert-danger mt-1">
            Monto mínimo a pagar {{ minimoMonto }}.
          </div>
        </field-messages>
      </validate>
      <br />
      <validate tag="div">
        <label for="pago">Pago</label>
        <input
          type="number"
          id="pago"
          name="pago"
          class="form-control"
          autocomplete="off"
          v-model.trim="formData.pago"
          required
          :min="minimoMonto"
        />

        <field-messages name="pago" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido
          </div>
          <div
            v-if="this.formData.pago < this.minimoMonto"
            slot="min"
            class="alert alert-danger mt-1"
          >
            No puede pagar menos que {{ minimoMonto }}.
          </div>
          <div
            v-if="Number(this.formData.pago) < Number(this.formData.monto)"
            class="alert alert-danger mt-1"
          >
            No puede pagar menos que lo que adeuda {{ this.formData.monto }}.
          </div>
        </field-messages>
      </validate>
      <button class="btn btn-success my-4" :disabled="formState.$invalid">
        Enviar
      </button>
 </vue-form>
 <button :class="mostrarTabla ? 'btn btn-danger' : 'btn btn-primary'" @click="verTabla()">{{mostrarTabla?'ocultar':'mostrar'}}</button>
      <table v-show="mostrarTabla" class="table table-dark"> <!-- aca cambia el display de block a none -->
      <!-- <table v-if="mostrarTabla" class="table table-dark"> aca aparece o desaparece la tabla-->
        <thead>
          <tr>
            <th>Nom</th>
            <th>Dni</th>
            <th>a pagar</th>
            <th>pagado</th>
            <th>fecha</th>
            <th>Saldo deuda</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(reg, index) in this.registros"
            :key="index"
            :style="{ background: getCol(reg) }"
          >
            <td>{{ reg.nombre }}</td>
            <td>{{ reg.documento }}</td>
            <td>{{ reg.monto }}</td>
            <td>{{ reg.pago }}</td>
            <td>{{ reg.fecha }}</td>
            <td>{{ reg.pago - reg.monto }}</td>
          </tr>
          <tr>
            <td>{{ this.formData.nombre }}</td>
            <td>{{ this.formData.documento }}</td>
            <td>{{ this.formData.monto }}</td>
            <td>{{ this.formData.pago }}</td>
          </tr>
        </tbody>
      </table>
   
  </section>
</template>

<script>
export default {
  name: "src-components-formulario",
  props: [],
  mounted() {},
  data() {
    return {
      nombreMinLength: 3,
      nombreMinLengthDoc: 7,
      nombreMaxLengthDoc: 8,
      minimoMonto: 0,
      formState: {},
      formData: this.getInicialData(),
      registros: [],
      mostrarTabla : false
    };
  },
  methods: {
    verTabla(){
      this.mostrarTabla = !this.mostrarTabla
    },
    getInicialData() {
      return {
        nombre: "",
        apellido: "",
        edad: "",
        email: "",
      };
    },
    enviar() {
      var fechaHora = new Date().toLocaleDateString();
      this.formData.fecha = fechaHora;
      this.registros.push(this.formData);
      this.formData = this.getInicialData();
      this.formState._reset();
    },
    getCol(regis) {
      var col;
      if (regis.pago - regis.monto > 0) {
        col = "blue";
      } else if (regis.pago - regis.monto == 0) {
        col = "green";
      } else {
        col = "red";
      }
      return col;
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
.src-components-formulario {
}
h1 {
  color: red;
}
</style>
