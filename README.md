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
import onOff from 'vue-on-off';

// register locally
const app = new Vue( {
	data(){
		return {
			model:false
		}
	}
	components:{
		onOff
	},
	methods:{
		toggleModel(){
			// some API request or other actions, you DON'T need to set model = !model
		}
	}
} );

// register globally
Vue.component('onOff',onOff);
```

```html
	<on-off v-model="model" :action="toggleModel"></on-off>
```
