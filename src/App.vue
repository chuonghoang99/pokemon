<template>
    <main-screen
        v-if="statusMatch === 'mainScreen'"
        @onStart="onHandleBeforeStart($event)"
    >
    </main-screen>

    <interact-screen
        v-if="statusMatch === 'interactScreen'"
        :cardContext="settings.cardContext"
    >
    </interact-screen>

    <result-screen v-if="statusMatch === 'resultScreen'"></result-screen>
</template>

<script>
import { shuffled } from './utils/array.js'
import MainScreen from './components/MainScreen.vue'
import InteractScreen from './components/InteractScreen.vue'
import ResultScreen from './components/ResultScreen.vue'
export default {
    name: 'App',
    components: {
        MainScreen,
        InteractScreen,
        ResultScreen,
    },
    data() {
        return {
            statusMatch: 'mainScreen',
            settings: {
                timeStart: null,
                totalBlock: 0,
                cardContext: [],
            },
        }
    },
    methods: {
        onHandleBeforeStart($event) {
            //console.log('envent', $event)

            this.settings.totalBlock = $event.totalBlock
            // console.log(this.settings.totalBlock)
            const firstCard = Array.from(
                { length: this.settings.totalBlock / 2 },
                (_, i) => i + 1
            )

            const card = [...firstCard, ...firstCard]
            this.settings.cardContext = shuffled(shuffled(card))
            console.log(this.settings.cardContext)
            console.log(card)

            //console.log(this.settings.totalBlock)
            this.settings.timeStart = new Date().getTime()
            this.statusMatch = 'interactScreen'
        },
    },
}
</script>

<style>
#app {
}
</style>
