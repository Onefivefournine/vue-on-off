<style>
//@extend-elements
%inner-before-after {
  display: block;
  float: left;
  width: 50%;
  padding: 0;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  height: 22px;
}

@mixin transition($args...) {
  -webkit-transition: $args;
  transition: $args;
}

$gray:#a3a6b2;
$green:#6ae2a2;
$lgray:darken(#f1f2f6, 5%);
.onoffswitch {
  position: relative;
  width: 50px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  &-checkbox {
    display: none;
    +.onoffswitch-label {
      border: 1px solid $lgray;
      @include transition(border 0.3s ease-in-out);
    }
    &:checked+.onoffswitch-label {
      border: 1px solid $green;
      @include transition(border 0.3s ease-in-out);
      .onoffswitch-inner {
        margin-left: 0;
      }
      .onoffswitch-switch {
        right: 2px;
      }
    }
    &[disabled]+.onoffswitch-label {
      border: 1px solid $lgray;
      cursor: not-allowed;
      .onoffswitch-inner:before {
        background-color: $gray;
      }
    }
  }
  &-label {
    display: block;
    overflow: hidden;
    cursor: pointer;
    margin-bottom: 0;
    border: 1px solid $green;
    border-radius: 100px;
  }
  &-inner {
    display: block;
    width: 200%;
    margin-left: -100%;
    @include transition(all 0.3s ease-in-out);
    &:before {
      @extend %inner-before-after;
      content: " ";
      background-color: $green;
    }
    &:after {
      @extend %inner-before-after;
      content: " ";
      background-color: $lgray;
    }
  }
  &-switch {
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
    @include transition(all 0.3s ease-in-out);
  }
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
      return 'onOff-' + ( Math.random() * 1000000 ).toFixed()
    }
  },
  watch: {
    innerModel( val ) {
      this.$emit( 'input', val )
      this.action()
    }
  },
  template
} );
</script>
