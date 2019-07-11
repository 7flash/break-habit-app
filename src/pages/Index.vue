<template>
<div class="q-pa-md">
  <q-stepper
    v-model="step"
    vertical
    color="primary"
    animated
  >
    <q-step
      :name="1"
      title="Select your goal"
      icon="settings"
      :done="step > 1"
    >
      Describe your goal in one sentence. You may want to create a new habit, for example: "Wakeup 4am" or "Stop smoking"

      <q-input v-model="goal" type="text"></q-input>

      <q-stepper-navigation>
        <q-btn @click="defineGoal()" color="primary" label="I defined my GOAL" />
      </q-stepper-navigation>
    </q-step>

    <q-step
      :name="2"
      title="Set your intention"
      caption="Optional"
      icon="settings"
      :done="step > 2"
    >
      Take a minute and Define your WHY for chosen goal, pronounce it loudly and then continue

      <q-stepper-navigation>
        <q-btn @click="defineWhy()" color="primary" label="I defined my WHY" />
        <q-btn flat @click="step = 1" color="primary" label="Back" class="q-ml-sm" />
      </q-stepper-navigation>
    </q-step>

    <q-step
      :name="3"
      title="Prepare for a battle"
      icon="settings"
      :done="step > 3"
    >
      <div class="text-subtitle">
        Whenever you have a choice to follow your heart and make a right choice, or fail back to old habit, - start a battle
      </div>
      <div class="text-subtitle">
        You will have 5 seconds to make the choice and receive reward, otherwise your money will start burning
      </div>
      <div class="text-subtitle">
        Follow your heart and make right choice to overcome old habit and build new behaviour, use additional tools on battle page
      </div>
      <div class="text-subtitle2">
        Your balance: {{ balance }} DDM
      </div>
      <div class="text-subtitle2">
        Your day: {{ day }}
      </div>
      <q-stepper-navigation>
        <q-btn @click="startBattle()" color="primary" label="START battle" />
        <q-btn flat @click="step = 2" color="primary" label="Back" class="q-ml-sm" />
      </q-stepper-navigation>
    </q-step>

    <q-step
      :name="4"
      title="Battle"
      icon="settings"
      :done="step > 4"
    >
      <div class="text-h4">
        SECONDS LEFT: {{ timer }}
      </div>
      <div class="text-h4">
        Your balance: {{ balance }}
      </div>

      <q-splitter
        v-model="splitterModel"
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

      <q-stepper-navigation>
        <q-btn @click="finishBattle()" color="primary" label="FINISH battle" />
      </q-stepper-navigation>
    </q-step>
  </q-stepper>
</div>
</template>

<style>
</style>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      balance: 50,
      day: 1,
      timer: 5,
      burner: null,
      goal: '',
      splitterModel: 50,
      step: 1
    }
  },
  methods: {
    defineGoal () {
      window.localStorage.setItem('goal', this.goal)
      this.step = 2
    },
    defineWhy () {
      this.step = 3
    },
    startBattle () {
      this.burner = setInterval(() => {
        if (this.timer > 0) {
          this.timer -= 1
        } else {
          if (this.balance > 0) {
            this.balance -= 1
          } else {
            this.balance = 50
            this.balance -= 1
          }
        }
      }, 1000)

      this.step = 4
    },
    finishBattle () {
      if (this.burner) {
        clearInterval(this.burner)
      }

      this.balance = Number.parseInt(this.balance) + 25
      this.$q.notify({ message: 'Congratulations! Your reward: +25 DDM' })
      window.localStorage.setItem('balance', this.balance)

      this.timer = 5
      this.step = 3
    }
  },
  mounted () {
    const goal = window.localStorage.getItem('goal')
    const day = window.localStorage.getItem('day')
    const step = window.localStorage.getItem('step')
    const balance = window.localStorage.getItem('balance')

    this.balance = balance || 0
    this.step = step || 1
    this.goal = goal || ''
    this.day = day || 1

    if (this.balance <= 0) {
      this.balance = 50
      window.localStorage.setItem('balance', this.balance)
      this.$q.notify({ message: 'Welcome! Your reward: +50 DDM' })
    }
  }
}
</script>
