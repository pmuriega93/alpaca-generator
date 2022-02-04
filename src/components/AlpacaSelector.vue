<template>
        <section class="alpaca__chars">
            <div class="chars-selector">
                <h3 class="selector-title">Choose accesories</h3>
                <ul>
                    <li
                    v-for="char in chars" :key="char.id"
                    class="chars-selector__item"
                    >
                        <a
                        @click="setOptions(char.label)"
                        class="selector-button">
                            {{char.label}}
                        </a>
                    </li>
                </ul>
            </div>

            <div class="option-selector">
                <h3 class="selector-title">{{optionsTitle}}</h3>
                <ul>
                    <li
                    v-for="option in options" :key="option.id"
                    class="chars-selector__item"
                    >
                        <a 
                        class="selector-button"
                        @click="setSelection(option)">{{option}}</a>
                    </li>
                </ul>
            </div>
        </section>
</template>

<script>
import alpacaParts from '@/helpers/alpacaParts.js'
export default {
    data() {
        return {
            chars: [],
            optionsTitle: '',
            options: [],
            selected: false,
        }
    },

    methods: {
        setOptions( val ) {
            this.options = []
            this.optionsTitle = val
            const selected = alpacaParts.find( a => a.label === val )
            
            for( let i = 0; i < selected.items.length; i++) {
                this.options.push(selected.items[i])
            }
        },

        setSelection( sel ) {
            const option = {
                label: this.optionsTitle,
                item: sel
            }
            this.$emit('setImage', option)
        }
    },

    mounted() {
        for(let i = 0; i < alpacaParts.length; i++) {
            this.chars.push({
                    label: alpacaParts[i].label,
            })
        }
    }
}
</script>

<style scoped>
    .alpaca__chars {
        display: grid;
        grid-template-rows: repeat(2, 1fr) 30rem;
        align-items: start;
    }

    .selector-title {
        font-size: 3.5rem;
        color: #89B0AE;
        text-align: left;
        margin-left: 1.5rem;
        text-transform: capitalize;
    }

    ul {
        list-style-type: none;
        display: flex;
        flex-wrap: wrap;
        gap: 2rem;
        padding: 1.5rem;
    }

    .chars-selector__item {
        cursor: pointer;
    }

    .selector-button {
        display: inline-block;
        padding: 1rem 2rem;
        font-size: 2rem;
        background-color: #BEE3DB;
        color: #555B6E;
        border-radius: 10px;
        transition: opacity .3s;
        text-transform: capitalize;
    }

    .selector-button:hover {
        opacity: .7;
    }

    .option-selector {
        display: flex;
        flex-wrap: wrap;
        justify-content: flex-start;
        flex-direction: column;
    }

    .selected {
        background-color: orangered;
    }

</style>