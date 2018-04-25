# Vue on-off switch component

### Installation

```
npm i -s vue-on-off
```

#### Or...

```
yarn add vue-on-off
```

#### Or...

```
git clone https://github.com/Onefivefournine/vue-on-off.git
```

### Usage
```javascript
// register locally
import onOff from 'vue-on-off';

const app = new Vue( {
	components:{
		onOff
	},
	data(){
		return {
			model:false
		}
	},
	methods:{
		modelChangeHandler(){
			/*
			* some API request or other actions,
			* you DON'T need to set model = !model
			*/
		}
	}
} );

// register globally
Vue.component('onOff',onOff);
```

```html
	<on-off v-model="model" :action="modelChangeHandler"></on-off>
```
