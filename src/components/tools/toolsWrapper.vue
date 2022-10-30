<template>
    <div class="tools">
        <h3>Tools:</h3>
        <hr />
        <div class="tools__item">
            <h4>Colors: </h4>
            <ul class="tools__colors">
                <ol
                    v-for="color, index in colors"
                    :key="index"
                >
                    <input type="color" id="head" name="head" :value="color" @change="changeColor($event, index)">
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
        title: {
            type: String,
            default: '',
        },
    },
    emits: ['update:colors'],
    setup(props, context) {
        const { colors, title  } = toRefs(props);
        const inputTitle = ref(title);

        function changeColor(e,id) {
            const res = colors.value;
            res[id] = String(e.target.value).toLocaleUpperCase();
            console.log(e.target.value , id);
            
            context.emit('update:colors', res);
        }

        return {
            changeColor,
            inputTitle,
        }
    }
  }
</script>

<style lang="scss">
    .tools {
        background: #232730;
        height: 300px;
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
    }
</style>
