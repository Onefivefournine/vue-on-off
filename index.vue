<style scoped>
.onoffswitch-inner:before,
.onoffswitch-inner:after {
  display: block;
  float: left;
  width: 50%;
  padding: 0;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  height: 22px;
}

.onoffswitch {
  position: relative;
  width: 50px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
}

.onoffswitch-checkbox {
  display: none;
}

.onoffswitch-checkbox+.onoffswitch-label {
  border: 1px solid #e1e4ec;
  -webkit-transition: border 0.3s ease-in-out;
  transition: border 0.3s ease-in-out;
}

.onoffswitch-checkbox:checked+.onoffswitch-label {
  border: 1px solid #6ae2a2;
  -webkit-transition: border 0.3s ease-in-out;
  transition: border 0.3s ease-in-out;
}

.onoffswitch-checkbox:checked+.onoffswitch-label .onoffswitch-inner {
  margin-left: 0;
}

.onoffswitch-checkbox:checked+.onoffswitch-label .onoffswitch-switch {
  right: 2px;
}

.onoffswitch-checkbox[disabled]+.onoffswitch-label {
  border: 1px solid #e1e4ec;
  cursor: not-allowed;
}

.onoffswitch-checkbox[disabled]+.onoffswitch-label .onoffswitch-inner:before {
  background-color: #a3a6b2;
}

.onoffswitch-label {
  display: block;
  overflow: hidden;
  cursor: pointer;
  margin-bottom: 0;
  border: 1px solid #6ae2a2;
  border-radius: 100px;
}

.onoffswitch-inner {
  display: block;
  width: 200%;
  margin-left: -100%;
  -webkit-transition: all 0.3s ease-in-out;
  transition: all 0.3s ease-in-out;
}

.onoffswitch-inner:before {
  content: " ";
  background-color: #6ae2a2;
}

.onoffswitch-inner:after {
  content: " ";
  background-color: #e1e4ec;
}

.onoffswitch-switch {
  display: block;
  width: 20px;
  height: 20px;
  margin: 2px 0 0;
  background: #fff;
  border-radius: 100%;
  position: absolute;
  top: 0;
  bottom: 0;
  right: 28px;
  -webkit-transition: all 0.3s ease-in-out;
  transition: all 0.3s ease-in-out;
}
</style>
<template>
  <div class="switch">
    <div class="onoffswitch">
      <input type="checkbox"
        class="onoffswitch-checkbox"
        v-model="innerModel"
        @input="action"
        :id="randomId">
      <label class="onoffswitch-label"
        :for="randomId">
        <span class="onoffswitch-inner"></span>
        <span class="onoffswitch-switch"></span>
      </label>
    </div>
  </div>
</template>
<script>
import Vue from 'vue';
export default Vue.extend( {
  data() {
    return {
      innerModel: this.value
    }
  },
  props: {
    value: {
      default: false
    },
    action: {
      type: Function,
      default: function() {}
    }
  },
  computed: {
    randomId() {
      return 'onOff-' + ( Math.random() * 1e9 ).toFixed()
    }
  },
  watch: {
    innerModel( val ) {
      this.$emit( 'input', val )
      this.action()
    }
  }
} );
</script>
