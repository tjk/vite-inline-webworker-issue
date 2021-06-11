<template>
  <div id="container"></div>
</template>

<script setup>
import { onMounted } from "vue"
import * as monaco from "monaco-editor"
import editorWorker from 'monaco-editor/esm/vs/editor/editor.worker?worker&inline'
import tsWorker from 'monaco-editor/esm/vs/language/typescript/ts.worker?worker&inline'

self.MonacoEnvironment = {
  getWorker(_, label) {
    if (label === "javascript") return tsWorker()
    return new editorWorker()
  },
}

onMounted(() => {
  monaco.editor.create(document.getElementById('container'), {
    value: "function hello() {\n\talert('Hello world!');\n}",
    language: "javascript",
  })
})
</script>

<style>
html {overflow:hidden}
html, body, #app, #container {height:100%;margin:0}
</style>
