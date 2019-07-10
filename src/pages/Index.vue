<template>
        <q-splitter
          v-model="splitterModel"
          style="width: 100%; height: 100%;"
          :limits="[0, 100]"
          before-class="overflow-hidden"
          after-class="overflow-hidden"
          separator-class="bg-black"
          separator-style="width: 25px;"
        >

          <template v-slot:before>
            <q-img
              src="assets/success.jpg"
            />
          </template>

          <template v-slot:after>
            <q-img
              src="assets/failure.jpg"
            />
          </template>

        </q-splitter>
</template>

<style>
</style>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      splitterModel: 50
    }
  }
}
</script>
