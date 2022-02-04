<template>

    <section class="alpaca__image">
        <div id="alpaca" class="avatar-container">
        <template v-for="(image, index) in imageSrc" :key="index">
            <img :class="image.label" :src="getPicture(index)" :alt="image.label">
        </template>
            <img class="nose" src="../assets/alpaca/nose.png" alt="nariz">
        </div>
        <div class="button-section">
            <button
            @click="randomize()"
            class="btn">
                <img class="icon" src="../assets/shuffle-variant.png" alt="download">
                Randomize
            </button>
            <button
            @click="download()"
            class="btn">
                <img class="icon" src="../assets/download-circle-outline.png" alt="download">
                Download
            </button>
        </div>
    </section>
</template>

<script>

import alpacaParts from '@/helpers/alpacaParts.js'
import domtoimage from 'dom-to-image-more';

export default {
    props: {
        selectedOption: {
            type: Object,
            required: false,
        },
    },
    
    data() {
        return {
          imageSrc: [],
        }
    },


    methods: {

        defaultImage() {
            for(let i = 0; i < alpacaParts.length; i++) {
                this.imageSrc.push({
                    label: alpacaParts[i].label,
                    item: alpacaParts[i].items[0]
                })
            }
            this.randomize()

        },

        setAccesories( label, item ) {
            const index = this.imageSrc.findIndex( a => a.label === label )
            this.imageSrc[index].label = label
            this.imageSrc[index].item = item
        },

        getPicture(index) {
            return require(`../assets/alpaca/${this.imageSrc[index].label}/${this.imageSrc[index].item}.png`)
        },

        randomize() {
            for(let i = 0; i < this.imageSrc.length; i++) {
                this.imageSrc[i].item = alpacaParts[i].items[Math.floor(Math.random() * alpacaParts[i].items.length)]
            }
        },

        download() {
            const node = document.getElementById('alpaca')
            domtoimage
                .toPng(node)
                .then((dataUrl) => {
                    let link = document.createElement("a")
                    link.download = "alpaca.png";
                    link.href = dataUrl;
                    link.click();
                })
        }
    },
    
    watch: {
        selectedOption(newVal, oldVal) {
            console.log(oldVal);
            const { label, item } = newVal
            this.setAccesories(label, item)
        }
    },


    mounted() {
        this.defaultImage()
    }

}
</script>

<style scoped>
    img {
        max-width: 100%;
        position: absolute;
        top: 0;
        left: 0;
    }

    .alpaca__image {
        display: grid;
        grid-template-areas: "image" "buttons";
        grid-template-rows: 1fr 150px;

    }

    .avatar-container {
        grid-area: "image";
        grid-row: 1 / span 1;
        position: relative;
    }

    .accessories {
        z-index: 20;
    }
    
    .eyes,
    .mouth {
        z-index: 20;
    }

    .button-section {
        position: relative;
        grid-row: 2 / -1;
        grid-area: "buttons";

    }

    .button-section > * {
        margin: 1.5rem;
        padding: 1rem 1.5rem;
    }

    .btn {
        display: inline-flex;
        gap: 1rem;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        color: #555B6E;
        background-color: #BEE3DB;
        border: none;
        border-radius: 10px;
        font-size: 2.5rem;
    }

    .btn > * {
        position: relative;
        height: 3rem;
    }

    .btn:hover {
        opacity: .75;
    }
</style>