<template>
  <div>
    <v-col cols="12">
      <v-sheet min-height="425px" rounded="xl" class="pa-5">
        <v-form ref="form" v-model="valid" lazy-validation>
          <v-row class="v-custom-row flex-wrap">
            <v-col xl="6" lg="6" md="6" sm="12" xs="12">
              <div class="form-label">
                <label>Откуда забирать?</label>
              </div>
              <v-text-field
                :rules="fromAddressRules"
                v-model="from_address"
                required
                hide-details="auto"
                placeholder="Введите адрес"
                solo
              >
                <v-tooltip top slot="append">
                  <template v-slot:activator="{ on, attrs }">
                    <span v-bind="attrs" v-on="on" class="icon-warning"> </span>
                  </template>
                  <span>Только на территории РФ</span>
                </v-tooltip>
              </v-text-field>
            </v-col>
            <v-col xl="6" lg="6" md="6" sm="12" xs="12">
              <div class="form-label">
                <label>Куда доставить?</label>
              </div>
              <v-text-field
                :rules="toAddressRules"
                v-model="to_address"
                required
                hide-details="auto"
                placeholder="Введите адрес"
                solo
              >
                <v-tooltip top slot="append">
                  <template v-slot:activator="{ on, attrs }">
                    <span v-bind="attrs" v-on="on" class="icon-warning"> </span>
                  </template>
                  <span>Только на территории РФ</span>
                </v-tooltip>
              </v-text-field>
            </v-col>
            <v-col xl="6" lg="6" md="6" sm="12" xs="12">
              <div class="form-label">
                <label class="form-label"> Объём перевозки</label>
              </div>
              <v-text-field
                :rules="transVolumeRules"
                v-model="trans_volume"
                required
                hide-details="auto"
                class="parent-outer-input"
                solo
                placeholder="Начните вводить"
              >
                <v-text-field
                  slot="append-outer"
                  placeholder="Тонна"
                  solo
                  :rules="transVolumeRules"
                  v-model="trans_volume_ton"
                  required
                  hide-details="auto"
                  class="outer-input m-0"
                >
                </v-text-field>
              </v-text-field>
            </v-col>
            <v-col xl="6" lg="6" md="6" sm="12" xs="12">
              <div class="form-label">
                <label>ФИО</label>
              </div>
              <v-text-field
                :rules="fullNameRules"
                v-model="full_name"
                required
                hide-details="auto"
                placeholder="Начните вводить"
                solo
              ></v-text-field>
            </v-col>

            <v-col xl="6" lg="6" md="6" sm="12" xs="12">
              <div class="form-label">
                <label>Телефон</label>
              </div>
              <v-text-field
                :rules="phoneNumberRules"
                v-model="phoneNumber"
                required
                v-mask="'+7-###-###-##-##'"
                placeholder="+7"
                hide-details="auto"
                solo
              ></v-text-field>
            </v-col>

            <v-col xl="6" lg="6" md="6" sm="12" xs="12">
              <div class="form-label">
                <label>e-mail</label>
              </div>
              <v-text-field
                :rules="emailRules"
                v-model="email"
                required
                hide-details="auto"
                placeholder="Начните вводить"
                solo
              ></v-text-field>
            </v-col>
          </v-row>
          <v-col class="px-0  form-action text-right">
            <v-btn @click="sendForm" outlined class="form-action__btn">
              Отправить
            </v-btn>
          </v-col>
        </v-form>
      </v-sheet>
    </v-col>
  </div>
</template>

<script>
export default {
  data() {
    return {
      valid: true,
      email: "",
      phoneNumber: "",
      full_name: "",
      from_address: "",
      to_address: "",
      trans_volume: "",
      trans_volume_ton: "",
      emailRules: [
        v => !!v || "Электронная почта обязательна",
        v =>
          /.+@.+\..+/.test(v) ||
          "Пожалуйста, введите действительный адрес электронной почты"
      ],
      fromAddressRules: [v => !!v || "Требуется адрес"],
      toAddressRules: [v => !!v || "Требуется адрес"],
      phoneNumberRules: [v => !!v || "Требуется номер телефона"],
      fullNameRules: [v => !!v || "Требуется ФИО"],
      transVolumeRules: [v => !!v || "Пожалуйста, заполните это поле"]
    };
  },
  methods: {
    sendForm() {
      let success = this.$refs.form.validate();
      if (success) {
        alert("Форма успешно отправлена");
        this.$refs.form.reset();
      } else {
        alert("Пожалуйста, заполните поля");
      }
    }
  }
};
</script>

<style>
.theme--light .parent-outer-input.v-text-field--solo .v-input__append-outer {
  margin: 0;
}
.theme--light
  .parent-outer-input.v-text-field--solo
  .v-input__append-outer
  .outer-input
  .v-input__control
  .v-input__slot
  .v-text-field__slot
  input::placeholder {
  color: #000;
  text-align: center;
  font-weight: 400;
}
.theme--light .parent-outer-input > .v-input__control {
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}
.theme--light .parent-outer-input > .v-input__control .v-input__slot {
  border-right: 1px solid rgba(204, 201, 201, 0.8);
}
.theme--light
  .parent-outer-input.v-text-field--solo
  .v-input__append-outer
  .outer-input
  > .v-input__control {
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
.theme--light
  .v-text-field--solo:not(.v-input--is-focused):not(.v-input--has-state)
  > .v-input__control
  > .v-input__slot
  fieldset {
  border: none;
  background: rgba(196, 196, 196, 0.2);
}
.theme--light
  .v-text-field.v-text-field--solo:not(.v-text-field--solo-flat)
  > .v-input__control
  > .v-input__slot {
  box-shadow: none;
  height: 55px;
  background: rgba(196, 196, 196, 0.2);
}
.v-text-field
  > .v-input__control
  > .v-input__slot
  > .v-text-field__slot
  input::placeholder {
  color: rgba(0, 0, 0, 0.4);
}
.theme--light .theme--light.v-icon {
  color: #66d0e8;
}
.theme--light .v-btn:not(.v-btn--round).v-size--default {
  height: unset;
  padding: 6px 18px 6px 24px;
  min-width: unset;
}
.form-action__btn:not(.form-action__btn--round).v-size--default {
  background-color: #66d0e8;
  border: none;
  font-weight: 300;
  text-transform: none;
  color: #fff;
}
</style>

<style lang="scss">
.outer-input {
  text-align: center;
}
.inputs-row {
  display: flex;
  align-items: flex-end;
}
.icon-warning {
  background-color: #66d0e8;
  height: 24px;
  border-radius: 50%;
  width: 24px;
  cursor: pointer;
  position: relative;
  &::after {
    position: absolute;
    content: "i";
    display: block;
    height: 100%;
    width: 100%;
    color: #000;
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
.form {
  &-label {
    margin-bottom: 8px;
  }
  &-action {
    margin-top: 33px;
  }
}
@media (max-width: 600px) {
  .v-custom-row {
    flex-direction: column;
  }
}
</style>
