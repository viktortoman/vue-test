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
        <div class="flex items-center justify-center h-screen" v-if="selectedData" v-show="toggle">
            <div class="rounded-border shadow border border-4 text-white w-3/5 p-3 break-words">
                <div class="box rounded-t-lg py-6 px-36 text-3xl text-center uppercase"
                     :style="{ 'background-color': selectedData.color }">
                    <span class="letter">{{ selectedData.name }}</span>
                </div>
                <div class="p-4 bg-white text-[#262626] text-center text-xl mt-3 mb-3 text-center">
                    <span class="letter">{{ selectedDataFrom + ' - ' + selectedDataTo  }}</span>
                </div>
                <div class="flex flex-row gap-2">
                    <div class="flex-1 box p-6 text-3xl" :class="getBorderClass(selectedData.talent, index)"
                         :style="{ 'background-color': selectedData.color }"
                         v-for="(talent, index) in selectedData.talent" :key="talent">
                        <span class="letter" :id="index">{{ talent }}</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import anime from "animejs";
import moment from "moment";
import data from '../assets/data.json'

export default {
    name: "MainComponent",
    props: {},
    data() {
        return {
            toggle: false,
            data: data,
            selectedData: {
                name: '',
                from: '',
                to: '',
                color: '',
                talent: [],
            },
            selectedDataFrom: '',
            selectedDataTo: '',
        }
    },
    mounted() {
        this.setSelectedData();
    },
    methods: {
        getBorderClass(talent, index) {
            if (talent.length === 1) {
                if (index === 0) {
                    return 'rounded-b-lg';
                }
            } else if (talent.length === 2) {
                if (index === 0) {
                    return 'rounded-bl-lg';
                }

                if (index === 1) {
                    return 'rounded-br-lg';
                }
            } else if(talent.length === 3) {
                if (index === 0) {
                    return 'rounded-bl-lg';
                }

                if (index === 2) {
                    return 'rounded-br-lg';
                }
            }
        },
        getRandomElement() {
            let randomIndex = Math.floor(Math.random() * this.data.length);
            return this.data[randomIndex] ? this.data[randomIndex] : null;
        },
        setSelectedData() {
            this.selectedData = this.getRandomElement() ? this.getRandomElement() : this.data[0];
            this.selectedDataTo = moment(this.selectedData.to).format("MMMM DD")
            this.selectedDataFrom = moment(this.selectedData.from).format("MMMM DD")
        },
        toggleData() {
            this.toggle = true
            this.setSelectedData();

            anime.timeline({loop: false})
                .add({
                    targets: '.letter',
                    scale: [7,1],
                    opacity: [0,1],
                    translateX: 250,
                    easing: "easeOutExpo",
                    duration: 1500,
                    delay: (el, i) => 30 * i
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

.box {
    text-shadow: 2px 2px 2px #0A0403;
    font-weight: 600;
    line-height: 0.9em;
    letter-spacing: -0.01em;
}
</style>