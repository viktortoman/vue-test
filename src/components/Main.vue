<template>
    <div id="app">
        <header class="pt-5 float-right">
            <button type="button"
                    class="text-white bg-green-700 hover:bg-green-800 focus:outline-none
                    focus:ring-4 focus:ring-green-300 font-medium rounded-full text-sm px-5 py-2.5
                    text-center mr-2 mb-2 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800"
                    @click="toggleData"
            >
                Toggle
            </button>
        </header>
        <div class="flex items-center justify-center h-screen" v-show="toggle">
            <div class="rounded-border shadow border border-4 text-white w-3/5 p-3 break-words">
                <div class="green-box rounded-t-lg py-6 px-36 text-3xl text-center uppercase">
                    <span class="letter">Rocket League Showdown 2020 Summer Shuffle</span>
                </div>
                <div class="p-4 bg-white text-[#262626] text-center text-xl mt-3 mb-3 text-center">
                    <span class="letter">June 29 - July 12</span>
                </div>
                <div class="flex flex-row gap-2">
                    <div class="flex-1 green-box rounded-bl-lg p-6 text-3xl">
                        <span class="letter">EterNaLeNvy</span>
                    </div>
                    <div class="flex-1 green-box p-6 text-3xl text-center">
                        <span class="letter">DakotaCox</span>
                    </div>
                    <div class="flex-1 green-box rounded-br-lg p-6 text-3xl text-right">
                        <span class="letter">Sarah Jessica Parker</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import anime from "animejs";
import {ref} from "vue";

export default {
    name: "MainComponent",
    props: {},
    data() {
        return {
            toggle: false,
        }
    },
    computed: {},
    methods: {
        toggleData() {
            this.toggle = true

            let letter = document.querySelector('.letter');
            letter.innerHTML = letter.textContent.replace(/\S/g, "<span class='letter'>$&</span>");

            anime.timeline({loop: false})
                .add({
                    targets: '.letter',
                    scale: [7,1],
                    opacity: [0,1],
                    translateZ: 120,
                    easing: "easeOutExpo",
                    duration: 1500,
                    delay: (el, i) => 70*i
                }).add({
                targets: '.ml2',
                opacity: 0,
                duration: 1000,
                easing: "easeOutExpo",
                delay: 10000
            });
        }
    }
}
</script>

<style scoped>
.rounded-border {
    -webkit-border-radius: 25px;
    -moz-border-radius: 25px;
    border-radius: 25px;
}

.green-box {
    background: #00D487;
    text-shadow: 2px 2px 2px #0A0403;
    font-weight: 600;
    line-height: 0.9em;
    letter-spacing: -0.01em;
}
</style>