<template>
  <div class="input_group">
    <div class="input">
      <input
        :type="type"
        :name="name"
        :placeholder="placeholder"
        @input="$emit('input',$event.target.value)"
      />
      <button
        href="javascript:;"
        v-if="btnText"
        :disabled="disabled"
        @click="$emit('btnClick')"
      >{{btnText}}</button>
    </div>
    <div class="err" v-if="error">{{error}}</div>
  </div>
</template>
<script>
export default {
  name: "InputGroup",
  props: {
    type: {
      type: String,
      default: "text"
    },
    name: String,
    placeholder: String,
    btnText: String,
    disabled: Boolean,
    error: String
  },
  methods: {
    aa() {
      alert(1);
    }
  }
};
</script>
<style scoped>
.input_group {
  width: 100%;
}
.input {
  width: 100%;
  position: relative;
}
.input input {
  width: 100%;
  height: 40px;
  border-radius: 4px;
  outline: none;
  border: 1px solid #ccc;
  font-size: 14px;
  box-sizing: border-box;
  padding-left: 5px;
  -webkit-appearance: none;
}
.input input:focus {
  border: 1px solid #1f8bda;
}
.input input::placeholder {
  color: #aaa;
  font-size: 14px;
}
.input button {
  position: absolute;
  right: 0;
  top: 0;
  height: 40px;
  display: inline-block;
  line-height: 40px;
  box-sizing: border-box;
  padding: 0px 10px;
  color: #bbb;
  text-decoration: none;
  background: rgba(255, 255, 255, 0);
  outline: none;
  border: none;
}
.err {
  font-size: 12px;
  color: #ff0000;
}
</style>
