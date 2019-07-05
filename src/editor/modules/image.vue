<template>
    <Dropzone
        :options="dropzoneOptions"
        :id="_uid+'vwdropzone'"
        ref="dropzone"
        @vdropzone-success="fileUploaded"
        @vdropzone-file-added="fileAdded"
        >
    </Dropzone>
</template>

<script>
import Dropzone from 'vue2-dropzone';
import bus from 'src/editor/bus.js';
// import 'vue2-dropzone/dist/vue2Dropzone.css'
import 'vue2-dropzone/dist/vue2Dropzone.min.css'

const UPLOAD_ICON = '<svg fill="#666" width="26" height="24" viewBox="0 0 2048 1792" xmlns="http://www.w3.org/2000/svg"><path d="M1344 864q0-14-9-23l-352-352q-9-9-23-9t-23 9l-351 351q-10 12-10 24 0 14 9 23t23 9h224v352q0 13 9.5 22.5t22.5 9.5h192q13 0 22.5-9.5t9.5-22.5v-352h224q13 0 22.5-9.5t9.5-22.5zm640 288q0 159-112.5 271.5t-271.5 112.5h-1088q-185 0-316.5-131.5t-131.5-316.5q0-130 70-240t188-165q-2-30-2-43 0-212 150-362t362-150q156 0 285.5 87t188.5 231q71-62 166-62 106 0 181 75t75 181q0 76-41 138 130 31 213.5 135.5t83.5 238.5z"/></svg>'

export default {
    title: "image",
    icon: '<svg style="width:18px;height:18px" viewBox="0 0 24 24"><path class="ql-fill" d="M19,19H5V5H19M19,3H5A2,2 0 0,0 3,5V19A2,2 0 0,0 5,21H19A2,2 0 0,0 21,19V5A2,2 0 0,0 19,3M13.96,12.29L11.21,15.83L9.25,13.47L6.5,17H17.5L13.96,12.29Z" /></svg>',
    description: "Insert Image",

    props: ["options"],
    components: {
        Dropzone
    },

    computed: {
        uploadURL () {
            return this.options.image.uploadURL;
        },

        dropzoneOptions () {
          return {
            // custom dropzone options
            ...this.options.image.dropzoneOptions,

            // vue2-dropzone config
            id: `${this._uid}vwdropzone`,
            url: this.uploadURL,
            autoProcessQueue: this.uploadURL !== 'None',
            dictDefaultMessage: `<i class="fa">${UPLOAD_ICON}</i><br>Click here to upload...`,

          }
        }
    },

    methods: {
        fileUploaded (file, r) {
            if (r)
                this.$emit("exec", "insertHTML", `<img src=${r}>`);
        },

        fileAdded (file) {
            // if no upload url is defined, insert image with base64 src
            if (file && this.uploadURL !== "None")
                return;

            const reader = new FileReader();

            reader.addEventListener("load", () => {
               this.$emit("exec", "insertHTML", `<img src=${reader.result}>`);
            }, false);

            reader.readAsDataURL(file);
        }
    },
}
</script>

