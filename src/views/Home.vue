<template>
  <h1>輸入內容:</h1>
  <!-- <div>wiuqrlw;eiO;IOEW</div> -->
  <div id="editorjs"></div>
  <button @click="save">存檔</button>
</template>

<script>
import EditorJS from "@editorjs/editorjs";
import Header from "@editorjs/header";
import List from "@editorjs/list";
import Embed from "@editorjs/embed";
import ImageTool from "@editorjs/image";
import Table from "@editorjs/table";
import DragDrop from "editorjs-drag-drop";
import Paragraph from "@editorjs/paragraph";
import AlignmentTuneTool from "editorjs-text-alignment-blocktune";
// import NestedList from "@editorjs/nested-list";

export default {
  name: "Home",
  data() {
    return {
      editor: "",
    };
  },
  mounted() {
    this.editor = new EditorJS({
      tools: {
        heading: {
          class: Header,
          inlineToolbar: ["link"],
          tunes: ["myTune"],
        },
        paragraph: {
          class: Paragraph,
          inlineToolbar: true,
          tunes: ["myTune"],
          config: {
            preserveBlank: true,
          },
        },
        list: {
          class: List,
          inlineToolbar: false,
        },
        // list: {
        //   class: NestedList,
        //   inlineToolbar: true,
        // },
        outLink: {
          class: Embed,
          config: {
            services: {
              youtube: true,
              twitter: true,
              facebook: true,
            },
          },
        },
        image: {
          class: ImageTool,
          config: {
            endpoints: {
              byFile: "http://localhost:8008/uploadFile", // Your backend file uploader endpoint
              byUrl: "http://localhost:8008/fetchUrl", // Your endpoint that provides uploading by Url
            },
          },
        },
        table: {
          class: Table,
          inlineToolbar: true,
        },
        myTune: {
          class: AlignmentTuneTool,
          // config: {
          //   default: "right",
          //   blocks: {
          //     header: "center",
          //     list: "right",
          //   },
          // },
        },
      },
      onReady: () => {
        new DragDrop(this.editor);
      },
    });
  },
  methods: {
    save() {
      this.editor.save().then((data) => {
        console.log(data.blocks);
      });
    },
  },
};
</script>
<style scoped lang="sass">
#editorjs
  background-color: #fff
  width: 80%
  margin: 0 auto
</style>
