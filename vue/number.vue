<script lang="ts" setup>
import JInput from "./Input.vue"
import type { CSSProperties } from 'vue';
import type { Property } from 'csstype';
import type { PropType } from 'vue';

enum Mode {
    column = "column",
    inline = "inline"
}

const props = defineProps({
    modelValue: {
        required: true,
        type: Number,
    },
    minValue: {
        type: Number,
        default: 0
    },
    maxValue: {
        type: Number,
        default: 9999
    },
    inputAlign: {
        type: String as PropType<Property.TextAlign>,
        default: "center"
    },
    inputWidth: {
        type: String,
        default: "100%"
    },
    mode: {
        type: String,
        default: Mode.inline
    },
    align: {
        type: String as PropType<Property.AlignItems>,
        default: "start"
    },
    label: {
        type: String,
        default: ""
    }
})

const divStyle: CSSProperties = {
    alignItems: props.align
}

const inputStyle: CSSProperties = {
    textAlign: props.inputAlign,
    width: props.inputWidth,
}

const emit = defineEmits(['update:modelValue'])
// const onInput: (e: Event) => void = (e) => {
//     if (e.target instanceof HTMLInputElement) {
//         let val = Number(e.target.value)
//         if (val < props.minValue) {
//             val = props.minValue
//         }
//         if (val > props.maxValue) {
//             val = props.maxValue
//         }
//         emit("update:modelValue", val)
//     }
// }

const onIncrease = () => {
    let val = props.modelValue + 1
    if (val > props.maxValue) {
        val = props.minValue
    }
    emit("update:modelValue", val)
}

const onDecrease = () => {
    let val = props.modelValue - 1
    if (val < props.minValue) {
        val = props.maxValue
    }
    emit("update:modelValue", val)
}

const inputValue = computed((): string => {
    return props.modelValue.toString()
})

onMounted(() => {
    console.log(props)
})

</script>


<template>
    <div class="j-input-number" :style="divStyle">
        <j-input :label="props.label" v-if="props.mode === Mode.inline" append v-model="inputValue"
            :style="inputStyle">
            <template #append>
                <div class="input-handle">
                    <v-btn density="comfortable" variant="flat" size="x-small" icon="mdi-chevron-up"
                        @click="onIncrease"></v-btn>
                    <v-btn density="comfortable" variant="flat" size="x-small" icon="mdi-chevron-down"
                        @click="onDecrease"></v-btn>
                </div>
            </template>
        </j-input>
        <template v-if="props.mode === Mode.column">
            <v-btn variant="flat" size="x-small" icon="mdi-chevron-up" @click="onIncrease"></v-btn>
            <j-input input-align="center" input-width="60px" :label="props.label" v-model="inputValue" />
            <v-btn variant="flat" size="x-small" icon="mdi-chevron-down" @click="onDecrease"></v-btn>
        </template>
    </div>
</template>

<style lang="scss" scoped>
.j-input-number {
    display: flex;
    flex-direction: column;
}

.input-handle {
    display: flex;
    flex-direction: column;
}</style>
