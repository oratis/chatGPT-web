<script setup lang="ts">
import useSetting from '@/composables/setting'
import { SettingOutlined } from '@ant-design/icons-vue'

const setting = useSetting()
const models = ref(['text-davinci-003', 'gpt-3.5-turbo'])

const props = defineProps<{
  visible: boolean
}>()

const emit = defineEmits(['update:visible'])

const visible = computed({
  get: () => props.visible,
  set: value => emit('update:visible', value)
})

const handleOk = () => {
  visible.value = false
  window.location.reload()
}


</script>

<template>
  <div>
    <a-modal v-model:visible="visible" @ok="handleOk" okText="确定" cancelText="关闭">
      <template #title>
        <SettingOutlined />
        <span class="ml-2">设置</span>
      </template>

      <a-form :model="setting">
        <a-form-item label="API_KEY">
          <a-input v-model:value="setting.app_key" placeholder="可替换为你的API_KEY，注意此举会替换本应用提供的KEY" />
        </a-form-item>
        <a-form-item label="连续对话">
          <a-switch v-model:checked="setting.continuously" checked-children="开" un-checked-children="关" />
        </a-form-item>
        <a-form-item label="对话模型">
          <a-select ref="select" v-model:value="setting.model" style="width: 180px">
            <a-select-option :value="model" v-for="model in models">{{ model }}</a-select-option>
          </a-select>
        </a-form-item>
      </a-form>


      <div class="mt-2"></div>





    </a-modal>
  </div>
</template>
