<template>
    <v-radio-group inline :model-value="modelValue" @change="onChange">
        <template v-for="item in options">
            <v-radio 
            color="red" 
            true-icon="mdi-circle"
            false-icon="mdi-circle-outline"  
            :label="item.label" 
            :value="item.value"></v-radio>
        </template>
    </v-radio-group>
</template>

<script lang="ts" setup>
const props = defineProps({
    modelValue: {
        required: true,
        type: Number,
    },
    options: {
        required: true,
        type: Array as PropType<{
            label: string,
            value: string|number
        }[]>,
        default: []
    },
})

const emit = defineEmits(['update:modelValue'])
const onChange = (e: any) => {
  emit("update:modelValue", Number(e.target.value))
}
</script>
