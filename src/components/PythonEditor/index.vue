<template>
  <div class="python-editor">
    <textarea ref="textarea" />
  </div>
</template>

<script>
import CodeMirror from 'codemirror'
import 'codemirror/addon/lint/lint.css'
import 'codemirror/lib/codemirror.css'
import 'codemirror/theme/rubyblue.css'
import 'codemirror/mode/javascript/javascript'
import 'codemirror/addon/lint/lint'
require('codemirror/mode/python/python.js')

export default {
  name: 'PythonEditor',
  props: ['value'],
  data() {
    return {
      PythonEditor: false
    }
  },
  mounted() {
    this.PythonEditor = CodeMirror.fromTextArea(this.$refs.textarea, {
      lineNumbers: true,
      mode: 'text/x-python',
      gutters: ['CodeMirror-lint-markers'],
      theme: 'rubyblue',
      lint: true
    })

    this.PythonEditor.setValue(this.value)
    this.PythonEditor.on('change', cm => {
      this.$emit('changed', cm.getValue())
      this.$emit('input', cm.getValue())
    })
  },
  methods: {
    getValue() {
      return this.PythonEditor.getValue()
    }
  }
}
</script>

<style scoped>
.python-editor{
  height: 100%;
  position: relative;
}
.python-editor >>> .CodeMirror {
  height: auto;
  min-height: 300px;
}
.python-editor >>> .CodeMirror-scroll{
  min-height: 300px;
}
.python-editor >>> .cm-s-rubyblue span.cm-string {
  color: #F08047;
}
</style>
