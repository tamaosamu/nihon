標誌
問題
合併請求
里程碑
探索
 
劉超
DEMO
/
nuxt3-demo
程式碼
問題
合併請求
套件
專案
版本發布
Wiki
動態
設定
nuxt3-demo/src/components/Checkbox.vue
45 行
1004 B
Vue
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
技術提供: Gitea
版本:
1.20.4+19-g2138661da
頁面:
107ms
模板:
10ms
授權條款
API
