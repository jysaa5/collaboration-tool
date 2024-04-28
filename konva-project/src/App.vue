<script setup lang="ts">
import StarterKit from "@tiptap/starter-kit";
import { useEditor, EditorContent } from "@tiptap/vue-3";
import html2canvas from "html2canvas";
import Konva from "konva";
import { Layer } from "konva/lib/Layer";
import { nextTick, onBeforeMount, onMounted, ref } from "vue";

const configKonva = {
  width: 500,
  height: 500,
};
const configCircle = {
  x: 100,
  y: 100,
  radius: 70,
  fill: "red",
  stroke: "black",
  strokeWidth: 4,
};
const layer = ref<Layer>();
const editor = useEditor({
  content: "<p>I’m running Tiptap with Vue.js. 🎉</p>",
  extensions: [StarterKit],
});

const shape = new Konva.Image({
  x: 0,
  y: 0,
  draggable: true,
  stroke: "red",
  scaleX: 1 / window.devicePixelRatio,
  scaleY: 1 / window.devicePixelRatio,
  image: undefined,
});

async function renderText() {
  console.log(editor.value?.getHTML());
  // convert DOM into image

  const div = document.getElementById("editor-container");
  console.log(div?.children[0]?.querySelector("p"));
  console.log(div);
  const div1 = document.getElementsByClassName("tiptap ProseMirror");
  console.log(div1);
  const list = Array.from(div1);
  console.log(list);

  // console.log(div?.querySelector("div p"));
  // console.log(div?.getElementsByClassName("tiptap ProseMirror")[0]);
  html2canvas(div as HTMLElement, {
    backgroundColor: "red",
    height: 100,
  }).then((canvas) => {
    // show it inside Konva.Image
    console.log("canvas", canvas);
    shape.image(canvas);
  });
}

onBeforeMount(() => {
  layer?.value?.add(shape);

  console.log(layer.value);
});

onMounted(async () => {
  await nextTick();
  await renderText();
});
</script>

<template>
  <v-stage :config="configKonva">
    <v-layer ref="layer">
      <v-circle :config="configCircle"></v-circle>
    </v-layer>
  </v-stage>
  <editor-content id="editor-container" :editor="editor" />
</template>
