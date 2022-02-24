<template>
  <span>
    <h1>File uploader</h1>
    <div>
      <label for="file">{{ label }}</label>
      <input
        id="file"
        type="file"
        :multiple="multiple"
        :accept="
          accept
            .split(' ')
            .map((i) => '.' + i)
            .join(', ')
        "
        ref="uploadInput"
        @change="handleChange()"
      />
    </div>
    <br />
    <pre>{{ fileMetaData }}</pre>
  </span>
</template>

<script>
// const reader = new FileReader();

// const conditon = map((i) => '.' + i).join(', ')
export default {
  props: {
    label: {
      type: String,
      require: false,
      default: "Upload Single File",
    },
    multiple: {
      type: Boolean,
      require: false,
      default: false,
    },
    accept: {
      // type: Array,
      require: false,
      default: "jpg",
    },
  },
  data() {
    return {
      fileMetaData: [],
      cool: {
        name: null,
        type: null,
        size: null,
        lastModified: null,
        lastModifiedDate: null,
        webkitRelativePath: null,
      },
    };
  },
  methods: {
    handleChange() {
      const uploadRef = this.$refs.uploadInput.files;
      for (const file of uploadRef) {
        const metaData = {
          name: file.name,
          type: file.type,
          size: file.size,
          lastModified: file.lastModified,
          lastModifiedDate: file.lastModifiedDate,
          webkitRelativePath: file.webkitRelativePath,
        };
        

        this.$data.fileMetaData.push(metaData);
      }
    },
  },
};
</script>

<style>
label {
  display: block;
  margin-bottom: 2rem;
}

/* [type="file"] {
  height: 0;
  overflow: hidden;
  width: 0;
}

[type="file"] + label {
  color: #fff;
  cursor: pointer;
  display: inline-block;
  font-family: "Rubik", sans-serif;
  font-size: inherit;
  font-weight: 500;
  margin-bottom: 1rem;

  padding: 1rem 50px;
  position: relative;
  transition: all 0.3s;
  vertical-align: middle;
}
[type="file"] + label.btn-2 {
  background-color: #41b883;
  border-radius: 50px;
  overflow: hidden;
}
[type="file"] + label.btn-2::before {
  color: #fff;
  content: "icon";

  font-size: 100%;
  height: 100%;
  right: 130%;
  line-height: 3.3;
  position: absolute;
  top: 0px;
  transition: all 0.3s;
}
[type="file"] + label.btn-2:hover {
  background-color: #497f42;
}
[type="file"] + label.btn-2:hover::before {
  right: 80%;
} */
</style>
