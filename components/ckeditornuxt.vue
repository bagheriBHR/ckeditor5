<template>
  <ckeditor
    :editor="editor"
    :value="value"
    :config="editorConfig"
    :tagName="tagName"
    :disabled="disabled"
    @input="event => $emit('input', event)"
  />
</template>
<script>

  let ClassicEditor
  let CKEditor

  if (process.client) {
    ClassicEditor = require('@honglm/ckeditor5-build-simple-upload')
    CKEditor = require('@ckeditor/ckeditor5-vue')
  } else {
    CKEditor = { component : {template:'<div></div>'}}
  }


  export default {
    name: "ckeditornuxt",
    components: {
      ckeditor: CKEditor.component
    },
    props: {
      value: {
        type: String,
        required: false
      },
      tagName: {
        type: String,
        required: false,
        default: 'div'
      },
      disabled: {
        type: Boolean,
        required: false,
      },
      uploadUrl: {
        type: String,
        required: false
      },
      config: {
        type: Object,
        required: false,
        default: function () {
        }
      }
    },
    data() {
      return {
        editor: ClassicEditor,
        editorConfig: {
          simpleUpload: {
            // The URL that the images are uploaded to.
            uploadUrl: "http://127.0.0.1:8000/api/v1/ckUpload",

            // Enable the XMLHttpRequest.withCredentials property.
            withCredentials: true,

            // Headers sent along with the XMLHttpRequest to the upload server.
            headers: {
            }
          }
        }
      }
    },
  };
</script>
