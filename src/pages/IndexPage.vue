<template>
  <q-page class="row justify-center items-center">
    <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md" style="width: 400px;">
      <q-input filled v-model="name" label="Your name" :rules="[val => !!val || 'Please type something']" />
      <q-input filled v-model="age" label="Your age" type="number" :rules="[val => val > 0 || 'Please type your age']" />
      <q-toggle v-model="accept" label="I accept terms and conditions" />
      <div class="row justify-between">
        <q-btn label="Submit" type="submit" color="primary" />
        <q-btn label="Reset" type="reset" color="secondary" flat />
      </div>
    </q-form>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'
import { useQuasar } from 'quasar'

const $q = useQuasar()
const name = ref('')
const age = ref(null)
const accept = ref(false)

function onSubmit () {
  if (accept.value) {
    $q.notify({ type: 'positive', message: 'Form submitted!' })
  } else {
    $q.notify({ type: 'negative', message: 'You need to accept terms.' })
  }
}

function onReset () {
  name.value = ''
  age.value = null
  accept.value = false
}
</script>