<style scoped>
.switch {
    display: inline-block;
}

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
    user-select: none;
}

.onoffswitch-checkbox {
    display: none;
}

.onoffswitch-checkbox:checked+.onoffswitch-label .onoffswitch-inner:after {
    background-color: #6ae2a2;
}

.onoffswitch-checkbox:checked+.onoffswitch-label .onoffswitch-switch {
    right: 2px;
}

.onoffswitch-checkbox[disabled]+.onoffswitch-label {
    cursor: not-allowed;
}

.onoffswitch-checkbox[disabled]+.onoffswitch-label .onoffswitch-inner:after {
    background-color: #dedede;
}

.onoffswitch-label {
    display: block;
    overflow: hidden;
    cursor: pointer;
    margin-bottom: 0;
    border-radius: 100px;
}

.onoffswitch-inner {
    display: block;
    width: 200%;
    -webkit-transition: all 0.3s ease-in-out;
    transition: all 0.3s ease-in-out;
}

.onoffswitch-inner:after {
    content: ' ';
    background-color: #e1e4ec;
    -webkit-transition: background-color 0.3s ease-in-out;
    transition: background-color 0.3s ease-in-out;
}

.onoffswitch-switch {
    display: block;
    width: 18px;
    height: 18px;
    margin: 2px 0 0;
    background: #fff;
    border-radius: 100%;
    position: absolute;
    top: 0;
    bottom: 0;
    right: 30px;
    -webkit-transition: all 0.3s ease-in-out;
    transition: all 0.3s ease-in-out;
}
</style>
<template>
    <div class="switch">
        <div class="onoffswitch">
            <input type="checkbox"
                   :disabled="disabled"
                   class="onoffswitch-checkbox"
                   v-model="innerModel"
                   @change="changeHandler"
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
export default {
    data() {
        return {
            innerModel: this.value
        };
    },
    props: {
        value: {
            default: false
        },
        disabled: {
            type: Boolean,
            default: false
        },
        action: {
            type: Function,
            default () {}
        }
    },
    computed: {
        randomId() {
            return `onOff-${(Math.random() * 1e9).toFixed()}`;
        }
    },
    watch: {
        value(val) {
            this.innerModel = val;
        }
    },
    methods: {
        changeHandler() {
            this.$emit('input', this.innerModel);
            this.$emit('change', this.innerModel);
            if (this.action && typeof this.action === 'function') this.action();
        }
    }
};
</script>
