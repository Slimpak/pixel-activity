<template>
    <div class="tools">
        <h3>Tools:</h3>
        <hr />
        <div class="tools__item">
            <h4>Draw mode: </h4>
            <input
                type="checkbox"
                id="head"
                name="head"
                :checked="false"
                @input="$emit('draw')"
            >

        </div>
        <hr />
        <div class="tools__item">
            <h4>Colors: </h4>
            <ul class="tools__colors">
                <ol
                    v-for="color, index in colors"
                    :key="index"
                >
                    <input
                        type="color"
                        id="head"
                        name="head" :value="color" @change="changeColor($event, index)"
                    >
                    <input type="radio" @input="$emit('activeColor', index)" :id="colors + index" name="colors" :value="index" :checked="Boolean(index === 0)">
                </ol>
            </ul>
        </div>
        <hr />
        <div class="tools__item">
            <h4>Title: </h4>
            <input
                class="tools__item-text"
                type="text"
                v-model="inputTitle"
                @input="$emit('update:title', $event.target.value)"
            >
        </div>
        <hr />
        <div class="tools__item">
            <h4>Number of years: </h4>
            <input
                class="tools__item-number"
                type="number"
                v-model="inputNumber"
                @input="$emit('update:countYears', $event.target.value)"
            >
        </div>
        <hr />
        <div class="tools__item">
            <h4>Fill random color: </h4>
            <button
                type="button"
                class="tools__item-number"
                @click="$emit('fill')"
            >
                Fill
            </button>
        </div>
        <hr />
        <div class="tools__item">
            <h4>Reset to back: </h4>
            <button
                type="button"
                class="tools__item-number"
                @click="$emit('reset')"
            >
                Reset
            </button>
        </div>
    </div>
</template>

<script>
import { toRefs, ref } from 'vue';

export default {
    name: 'toolsWrapper',
    props: {
        colors: {
            type: Array,
            default: () => [],
        },
        activeDraw: {
            type: Object,
            default: () => {},
        },
        countYears: {
            type: Number,
            default: 0,
        },
        title: {
            type: String,
            default: '',
        },
    },
    emits: ['update:colors', 'update:countYears', 'reset', 'fill', 'update:activeDraw', 'activeColor'],
    setup(props, context) {
        const { colors, title  } = toRefs(props);
        const inputTitle = ref(title);
        const inputNumber = ref(3);

        function changeColor(e,id) {
            const res = colors.value;
            res[id] = String(e.target.value).toLocaleUpperCase();
            console.log(e.target.value , id);
            
            context.emit('update:colors', res);
        }

        return {
            changeColor,
            inputTitle,
            inputNumber,
        }
    }
  }
</script>

<style lang="scss">
    .tools {
        background: #232730;
        min-height: 300px;
        position: fixed;
        right: 0;
        top: 0;
        width: 150px;
        border: 1px solid #545578;
        padding: 10px 15px;

        &__colors {
            margin: 4px 0;
            display: flex;
            flex-direction: column;
            gap: 8px;

            ol {
                display: flex;
                gap: 16px;
            }
        }

        hr {
            opacity: .5;
        }

        &__item {
            margin: 8px 0;
        }

        ul, ol, li {
            padding: 0;
            list-style-type: none;
        }

        &__item-text {
            margin: 4px 0;
            width: 80px;
            border: 1px solid #fff;
            background: #ffffff00;
            color: white;
        }

        &__item-number {
            margin: 4px 0;
            width: 80px;
            border: 1px solid #fff;
            background: #ffffff00;
            color: white;
        }
    }
</style>
