<template>
	<div id="app" :style="'background:linear-gradient(' + deg +'deg,' + finalGradient + ');'">
		<div class="container">
			{{ finalGradient }}

			<label>
				<input type="text" value="9CECFB"/>
			</label>
			<label>
				<input type="text" value="65C7F7"/>
			</label>
			<label v-for="(input,index) in inputs">
				<input type="text" v-model="input.color" :style="'color:' + input.color"/>
				<button @click="deleteRow(index)">-</button>
			</label>


			<button @click="addInput">+</button>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			deg: 45,
			gradients: ['#12c2e9, #c471ed, #f64f59'],
			finalGradient: '',
			inputs:[],
			number: 0


		}
	},
	created(){
		this.applyGradient();
	},
	methods:{
		applyGradient(){
			var arr = this.gradients;
			this.finalGradient = arr.toString();
		},
		addInput(){
			if(this.number >= 3) return;
			this.number++
			this.inputs.push({
				color: this.rainbow()
			});
		},
		deleteRow(index) {
			this.inputs.splice(index,1);
		},
		rainbow() {
			// // This function generates vibrant, "evenly spaced" colours (i.e. no clustering). This is ideal for creating easily distinguishable vibrant markers in Google Maps and other apps.
			// // Adam Cole, 2011-Sept-14
			// // HSV to RBG adapted from: http://mjijackson.com/2008/02/rgb-to-hsl-and-rgb-to-hsv-color-model-conversion-algorithms-in-javascript
			// var x = Math.floor((Math.random() * 100) + 1);
			// var y = Math.floor((Math.random() * 100) + 1);
			// var r, g, b;
			// var h = x / y;
			// //var h = step / numOfSteps;
			// var i = ~~(h * 6);
			// var f = h * 6 - i;
			// var q = 1 - f;
			// switch(i % 6){
			// 	case 0: r = 1; g = f; b = 0; break;
			// 	case 1: r = q; g = 1; b = 0; break;
			// 	case 2: r = 0; g = 1; b = f; break;
			// 	case 3: r = 0; g = q; b = 1; break;
			// 	case 4: r = f; g = 0; b = 1; break;
			// 	case 5: r = 1; g = 0; b = q; break;
			// }
			// var c = "#" + ("00" + (~ ~(r * 255)).toString(16)).slice(-2) + ("00" + (~ ~(g * 255)).toString(16)).slice(-2) + ("00" + (~ ~(b * 255)).toString(16)).slice(-2);
			// return (c);

			var randomColor = "#000000".replace(/0/g,function(){return (~~(Math.random()*16)).toString(16);});

			return randomColor;
		}
	}
}
</script>

<style lang="scss">
* {
    box-sizing: border-box;
}
html {
    margin: 0;
    padding: 0;
	height: 100%;
	min-height:100%;
}
body {
    padding: 0;
    margin: 0;
	height: 100%;
	min-height:100%;
	overflow:auto;
}
#app {
	font-family: "Avenir", Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;

	height:100%;
	display: flex;
	justify-content: center;
	align-items: center;
	background:#dedede;
	.container{
		background:rgba(255,255,255,0.1);
		text-align: center;
		padding:25px;
		max-width: 600px;
		width: 100%;
		border:1px solid #ffffff;
		border-radius:10px;
		&:hover{
			transition: 0.1s ease-in-out;
			background:rgba(255,255,255,0.5);
		}
		label{
			width: 100%;
			display: block;
			padding:10px;
			input{
				height:60px;
				box-shadow: none;
				border:0;
				border-radius: 5px;
				max-width: 400px;
				width: 100%;
				text-align: center;
				font-weight: 600;
				font-size: 30px;
			}
		}

	}
}
</style>
