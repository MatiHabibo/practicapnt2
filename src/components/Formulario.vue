<template>
  <section class="src-components-formulario">
    <h1>Formulario de pagos</h1>

    <vue-form :state="formState" @submit.prevent="enviar()">
      <!-- --------------------- -->
      <!--     Campo nombre      -->
      <!-- --------------------- -->
      <validate tag="div">
        <!-- Elemento de entrada -->
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
        <!-- Elemento de entrada -->
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
      <br>
      <validate tag="div">
        <!-- Elemento de entrada -->
        <label for="monto">Monto a pagar</label>
        <input
          type="number"
          id="monto"
          name="monto"
          class="form-control"
          autocomplete="off"
          v-model.trim="formData.monto"
          required
          :min = "minimoMonto"
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
       <br>
      <validate tag="div">
        <!-- Elemento de entrada -->
        <label for="pago">Pago</label>
        <input
          type="number"
          id="pago"
          name="pago"
          class="form-control"
          autocomplete="off"
          v-model.trim="formData.Pago"
          required
          :min = "minimoMonto"
        />

        <field-messages name="pago" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">
            Campo requerido
          </div>
          <div slot="min" class="alert alert-danger mt-1">
             No puede pagar menos que {{ minimoMonto }}.
            <div v-if="this.pagoMin < this.formData.monto">
               No puede pagar menos que lo que adeuca {{ pagoMin }}.
            </div>
           
          </div>
        </field-messages>
      </validate>
      <button class="btn btn-success my-4" :disabled="formState.$invalid">
        Enviar
      </button>
    </vue-form>
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
    };
  },
  methods: {
    getInicialData() {
      return {
        nombre: "",
        apellido: "",
        edad: "",
        email: "",
      };
    },
    enviar() {
      this.formData = this.getInicialData();
      this.formState._reset();
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
