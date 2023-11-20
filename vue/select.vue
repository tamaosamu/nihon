<template>
    <v-select density="compact" :items="props.options" item-title="label" item-value="value" variant="solo"
        :model-value="props.modelValue" return-object @update:modelValue="onChange"></v-select>
</template>

<script lang="ts" setup>
import type { PropType } from 'vue';

export type Option = {
    label: string
    value: string | number
}

const props = defineProps({
    modelValue: {
        required: true,
        type: [String, Number],
    },
    options: {
        required: true,
        type: Array as PropType<Option[]>,
        default: []
    },
})

const emit = defineEmits(['update:modelValue'])
const onChange = (option: Option | null) => {
    if (option) {
        emit("update:modelValue", option.value)
    }
}

</script>

<style lang="scss">
.v-select {

    .v-field--variant-solo,
    .v-field--variant-solo-filled {
        border: 1px solid #CCC;
        box-shadow: none
    }
}
</style>
