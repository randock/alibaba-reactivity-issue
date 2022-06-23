<template>
  <FormProvider :form="form">
    <SchemaField
        :schema="{
        type: 'object',
        properties: {
          toggle: {
            type: 'string',
            'x-component': 'Input',
            required: true
          },
          objectVisible: {
            'x-reactions': [
                {
                  dependencies: ['toggle'],
                  fulfill: {
                    state: {
                      visible: '{{$deps[0] !==\'hide\'}}'
                    }
                  }
                }
            ],
            type: 'object',
            properties: {
              test: {
                type: 'string',
                'x-component': 'Input'
              }
            }
          }
        },
      }"
    >
    </SchemaField>
    <FormConsumer>
      <template #default="{ form }">
        <div style="white-space: pre">
          {{ JSON.stringify(form.values, null, 2) }}
        </div>
      </template>
    </FormConsumer>
  </FormProvider>
</template>

<script>
import { Input } from 'ant-design-vue'
import { createForm, setValidateLanguage } from '@formily/core'
import {
  FormProvider,
  FormConsumer,
  createSchemaField,
} from '@formily/vue'
import 'ant-design-vue/dist/antd.css'

setValidateLanguage('en')

const { SchemaField } = createSchemaField({
  components: {
    Input,
  },
})

export default {
  components: {
    FormProvider,
    FormConsumer,
    SchemaField,
  },
  data() {
    const form = createForm({ validateFirst: true })

    return {
      form,
    }
  },
}
</script>
