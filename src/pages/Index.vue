<template>
  <q-page class="flex flex-center">
    <q-card class="my-card">
      <q-card-section>
        <form @submit.prevent.stop="onSubmit" @reset.prevent.stop="onReset">
          <q-input 
            ref="inputNumber"
            standout="bg-teal text-white" 
            v-model="inputNumber" 
            label="عدد در مبنای دودویی:"
            mask="########"
            lazy-rules
            :rules="[ val => /^[0-1]{1,8}$/.test(val) || 'فقط اعداد ۰ و ۱ مجاز به استفاده هستند' ]"
          />

          <div class="text-center">
            <q-btn label="محاسبه" type="submit" color="primary" />
          </div>
        </form>
      </q-card-section>
      <q-card-section>
        <div v-if="hidden"  class="text-center">
          عدد در مبنای دهدهی:
          {{ answer }}
        </div>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data() {
    return {
      inputNumber: '',
      answer: 0,
      hidden: false,
    }
  },
  methods: {
    onSubmit() {
      this.$refs.inputNumber.validate()

      if (this.$refs.inputNumber.hasError) {
        this.formHasError = true
      }
      else {
        this.answer = 0
        this.answer += parseInt(this.inputNumber, 2)
        this.hidden = true
      }
    }
  }
}
</script>