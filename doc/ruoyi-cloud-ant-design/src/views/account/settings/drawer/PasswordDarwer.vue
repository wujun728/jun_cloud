<template>
  <div>
    <a-drawer
      title="安全设置-修改密码"
      :width="640"
      :visible="visible"
      :confirmLoading="loading"
      @ok="() => { $emit('ok') }"
      @close="() => { $emit('cancel') }"
    >
      <a-form :form="form" :label-col="{ span: 5 }" :wrapper-col="{ span: 12 }" @submit="handleSubmit">
        <a-form-item label="旧密码">
          <a-input
            type="password"
            v-decorator="['oldPassword', { rules: [{ required: true, message: '旧密码不能为空!' }] }]"
          />
        </a-form-item>
        <a-form-item label="新密码">
          <a-input
            type="password"
            v-decorator="['newPassword', { rules: [{ required: true, message: '新密码不能为空!' }] }]"
          />
        </a-form-item>
        <a-form-item label="确认密码">
          <a-input
            type="password"
            v-decorator="['newPassword2', { rules: [{ required: true, message: '确认密码不能为空!' }] }]"
          />
        </a-form-item>
      </a-form>

      <div
        :style="{
          position: 'absolute',
          bottom: 0,
          width: '100%',
          borderTop: '1px solid #e8e8e8',
          padding: '10px 16px',
          textAlign: 'right',
          left: 0,
          background: '#fff',
          borderRadius: '0 0 4px 4px',
        }"
      >
        <a-button style="marginRight: 8px" @click="() => { $emit('cancel') }">
          取消
        </a-button>
        <a-button type="primary" @click="() => { $emit('ok') }">
          确认修改
        </a-button>
      </div>
    </a-drawer>
  </div>
</template>
<script>
export default {
  props: {
    visible: {
      type: Boolean,
      required: true
    },
    loading: {
      type: Boolean,
      default: () => false
    },
    model: {
      type: Object,
      default: () => null
    }
  },
  data () {
    return {
      // visible: false,
      childrenDrawer: false,
      formLayout: 'horizontal',
      form: this.$form.createForm(this, { name: 'coordinated' })
    }
  },
  methods: {
    handleSubmit (e) {
      e.preventDefault()
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log('Received values of form: ', values)
        }
      })
    },
    handleSelectChange (value) {
      this.form.setFieldsValue({
        note: `Hi, ${value === 'male' ? 'man' : 'lady'}!`
      })
    }
  }
}
</script>
