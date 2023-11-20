
<template>
   <div class="j-checkbox">
    <template v-for="item in options">
            <v-checkbox 
            color="red" 
            true-icon="mdi-circle"
            false-icon="mdi-circle-outline"  
            :label="item.label" 
            :value="item.value"
            :model-value="modelValue"
            @update:modelValue="onChange"
            ></v-checkbox>
        </template>
   </div>
     
</template>

<script lang="ts" setup>
type ModelValue = null|string[]|number[]
const props = defineProps({
    modelValue: {
        required: true,
        type: Array as PropType<ModelValue>,
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
const onChange = (value: ModelValue) => {
  emit("update:modelValue", value)
}
</script>

<style lang="scss" scoped>
.j-checkbox {
    display: flex;
}
</style>
