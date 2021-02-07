<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6 mb-4">
        <div class="card mb-3">
          <h5 class="card-header card-primary mb-4 bg-primary text-white">
            Image Compress
          </h5>
          <div class="card-body">
            <input
              class="form-control"
              type="file"
              id="file"
              ref="file"
              v-on:change="onChangeFileUpload()"
            />

            <div class="text-center mt-2">
              <button
                data-id="000"
                class="btn btn-success"
                type="button"
                @click="compress()"
              >
                Compress Image
              </button>
            </div>

            <p class="mt-5" id="inputTitle"></p>
            <img src="" id="inputURL" class="img-fluid" />
          </div>
        </div>
      </div>

      <div class="col-lg-6 mb-4">
        <div class="card h-100">
          <h4 class="card-header bg-primary text-white">Options</h4>
          <div class="card-body">
            <fieldset class="form-group">
              <div class="form-check form-check-inline">
                <input
                  type="checkbox"
                  name="strict"
                  id="inputStrict"
                  class="form-check-input"
                  v-model="options.strict"
                />
                <label for="inputStrict" class="form-check-label">strict</label>
              </div>
            </fieldset>
            <fieldset class="form-group">
              <div class="form-check form-check-inline">
                <input
                  type="checkbox"
                  name="checkOrientation"
                  id="inputCheckOrientation"
                  class="form-check-input"
                  v-model="options.checkOrientation"
                />
                <label for="inputCheckOrientation" class="form-check-label"
                  >checkOrientation</label
                >
              </div>
            </fieldset>
            <div class="form-group row">
              <label for="inputMaxWidth" class="col-5 col-form-label"
                >maxWidth</label
              >
              <div class="col-7">
                <input
                  type="number"
                  name="maxWidth"
                  id="inputMaxWidth"
                  placeholder="Infinity"
                  class="form-control"
                  v-model="options.maxWidth"
                />
              </div>
            </div>
            <div class="form-group row">
              <label for="inputMaxHeight" class="col-5 col-form-label"
                >maxHeight</label
              >
              <div class="col-7">
                <input
                  type="number"
                  name="maxHeight"
                  id="inputMaxHeight"
                  placeholder="Infinity"
                  class="form-control"
                  v-model="options.maxHeight"
                />
              </div>
            </div>
            <div class="form-group row">
              <label for="inputMinWidth" class="col-5 col-form-label"
                >minWidth</label
              >
              <div class="col-7">
                <input
                  type="number"
                  name="minWidth"
                  id="inputMinWidth"
                  placeholder="0"
                  class="form-control"
                  v-model="options.minWidth"
                />
              </div>
            </div>
            <div class="form-group row">
              <label for="inputMinHeight" class="col-5 col-form-label"
                >minHeight</label
              >
              <div class="col-7">
                <input
                  type="number"
                  name="minHeight"
                  id="inputMinHeight"
                  placeholder="0"
                  class="form-control"
                  v-model="options.minHeight"
                />
              </div>
            </div>
            <div class="form-group row">
              <label for="inputWidth" class="col-5 col-form-label">width</label>
              <div class="col-7">
                <input
                  type="number"
                  name="width"
                  id="inputWidth"
                  placeholder="undefined"
                  class="form-control"
                  v-model="options.width"
                />
              </div>
            </div>
            <div class="form-group row">
              <label for="inputHeight" class="col-5 col-form-label"
                >height</label
              >
              <div class="col-7">
                <input
                  type="number"
                  name="height"
                  id="inputHeight"
                  placeholder="undefined"
                  class="form-control"
                  v-model="options.height"
                />
              </div>
            </div>
            <div class="form-group row">
              <label for="inputQuality" class="col-5 col-form-label"
                >quality</label
              >
              <div class="col-7">
                <select
                  name="quality"
                  id="inputQuality"
                  class="form-control"
                  v-model="options.quality"
                >
                  <option value="0">0</option>
                  <option value="0.1">0.1</option>
                  <option value="0.2">0.2</option>
                  <option value="0.3">0.3</option>
                  <option value="0.4">0.4</option>
                  <option value="0.5">0.5</option>
                  <option value="0.6">0.6</option>
                  <option value="0.7">0.7</option>
                  <option value="0.8">0.8</option>
                  <option value="0.9">0.9</option>
                  <option value="1">1</option>
                </select>
              </div>
            </div>
            <div class="form-group row">
              <label for="inputMimeType" class="col-5 col-form-label"
                >mimeType</label
              >
              <div class="col-7">
                <input
                  type="text"
                  name="mimeType"
                  id="inputMimeType"
                  placeholder="auto"
                  class="form-control"
                  v-model="options.mimeType"
                />
              </div>
            </div>
            <div class="form-group row mb-0">
              <label for="inputConvertSize" class="col-5 col-form-label"
                >convertSize</label
              >
              <div class="col-7">
                <input
                  type="number"
                  name="convertSize"
                  id="inputConvertSize"
                  placeholder="5000000"
                  class="form-control"
                  v-model="options.convertSize"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-12 mb-4" v-if="suc">
        <div class="card mb-3">
          <h5 class="card-header card-primary bg-primary text-white">Result</h5>
          <div class="card-body">
            <img src="" id="outputURL" class="img-fluid" />
            <div class="table-responsive">
              <table class="table mb-3 mt-4 text-left">
                <tbody>
                  <tr>
                    <th scope="row">lastModified:</th>
                    <td id="lastModified"></td>
                  </tr>
                  <tr>
                    <th scope="row">lastModifiedDate:</th>
                    <td id="lastModifiedDate"></td>
                  </tr>
                  <tr>
                    <th scope="row">name:</th>
                    <td id="name"></td>
                  </tr>
                  <tr>
                    <th scope="row">type:</th>
                    <td id="type"></td>
                  </tr>
                  <tr>
                    <th scope="row">size:</th>
                    <td id="size"></td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Compressor from "compressorjs";
export default {
  name: "HelloWorld",
  data() {
    return {
      file: "",
      inputURL: "",
      outputURL: "",
      input: {},
      output: {},
      suc: false,
      options: {
        strict: true,
        checkOrientation: true,
        maxWidth: undefined,
        maxHeight: undefined,
        minWidth: 0,
        minHeight: 0,
        width: undefined,
        height: undefined,
        quality: 0.3,
        mimeType: "",
        convertSize: 5000000,
        success: function (result) {
          function humanFileSize(bytes, si = false, dp = 1) {
            const thresh = si ? 1000 : 1024;

            if (Math.abs(bytes) < thresh) {
              return bytes + " B";
            }

            const units = si
              ? ["kB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB"]
              : ["KiB", "MiB", "GiB", "TiB", "PiB", "EiB", "ZiB", "YiB"];
            let u = -1;
            const r = 10 ** dp;

            do {
              bytes /= thresh;
              ++u;
            } while (
              Math.round(Math.abs(bytes) * r) / r >= thresh &&
              u < units.length - 1
            );

            return bytes.toFixed(dp) + " " + units[u];
          }

          let date = new Date(result.lastModified);
          document.getElementById("outputURL").src = URL.createObjectURL(
            result
          );
          document.getElementById("lastModified").innerHTML =
            result.lastModified;
          document.getElementById("lastModifiedDate").innerHTML = date;
          document.getElementById("name").innerHTML = result.name;
          document.getElementById("type").innerHTML = result.type;
          document.getElementById("size").innerHTML = humanFileSize(
            result.size
          );
        },
        error: function (err) {
          window.alert(err.message);
        },
      },
    };
  },
  methods: {
    onChangeFileUpload() {
      this.file = this.$refs.file.files[0];
      document.getElementById("inputURL").src = URL.createObjectURL(this.file);
      document.getElementById("inputTitle").innerHTML =
        this.file.name + " (" + this.humanFileSize(this.file.size) + ")";
    },
    compress() {
      console.log(this.file);
      let com = new Compressor(this.file, this.options);
      console.log(com);
      if (!com.aborted) {
        this.suc = true;
      }
    },
    humanFileSize(bytes, si = false, dp = 1) {
      const thresh = si ? 1000 : 1024;

      if (Math.abs(bytes) < thresh) {
        return bytes + " B";
      }

      const units = si
        ? ["kB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB"]
        : ["KiB", "MiB", "GiB", "TiB", "PiB", "EiB", "ZiB", "YiB"];
      let u = -1;
      const r = 10 ** dp;

      do {
        bytes /= thresh;
        ++u;
      } while (
        Math.round(Math.abs(bytes) * r) / r >= thresh &&
        u < units.length - 1
      );

      return bytes.toFixed(dp) + " " + units[u];
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
