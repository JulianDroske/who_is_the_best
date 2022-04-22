<template>
	<div class="list-main">
		<div class="title-container">
			<div class="title">
				{{TYPES[type].title}}
			</div>
			<div class="comment">
				<textarea ref="commenta" name="commenta" rows="5" placeholder="Press Enter to add comment"
					v-model="commentText" @keydown="handleCommenta"></textarea>
			</div>
		</div>
		<div class="list-main-container">
			<div class="list-main-item"
				v-for="com in comments" :key="com.id" :style="{background: COLORS[com.bgcolor]}">
				<div class="list-stararea">

				</div>
				<span class="list-content">{{com.content}}</span>
				<div class="list-info">

				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'ListView',
	data(){
		return {
			TYPES:{
				good: {
					title: 'Went well'
				},
				so: {
					title: 'To improve'
				},
				todo: {
					title: 'Action items'
				}
			},
			COLORS:[
				'#ffeccc',
				'#e9ffcc',
				'#ccfdff',
				'#ccd0ff',
				'#feccff'
			],
			comments: [
				{
					id: 'sys-1',
					content: 'Hello!',
					bgcolor: 0
				},
				{
					id: 'sys-2',
					content: 'World!',
					bgcolor: 1
				}
			],
			commentText: ''
		}
	},
	props: {
		type: String
	},
	mounted(){
		let localData = null;
		if(localData = localStorage.getItem(this.type)){
			this.comments = JSON.parse(localData);
		}
	},
	methods: {
		handleCommenta(event){
			if(event.keyCode == 13){
				if(event.ctrlKey){
					this.commentText = this.commentText + '\n';
				}else{
					event.preventDefault();
					var text = this.commentText;
					this.commentText = '';
					this.addComment(text);
				}
			}
		},
		genId(){
			return Array.from({length: 8}).
				map(val=>(Math.random()*10)|0).
				join('');
		},
		addComment(text){
			if(text){
				this.comments.unshift({
					id: this.genId(),
					content: text,
					bgcolor: (Math.random()*this.COLORS.length)|0
				});
				localStorage.setItem(this.type, JSON.stringify(this.comments))
			}
		}
	}
}
</script>

<style scoped>

textarea {
	width: 100%;
	border: none;
	padding: 0.5em;
	resize: none;
	outline: 1px blue;
	box-sizing: border-box;
	background: transparent;
}

.list-main {
	display: flex;
	flex-direction: column;
	height: fit-content;	/* bug? */
	padding: 0px 1em 1em 1em;
	font-family: 'Ubuntu Mono';
	border: 1px solid rgb(233, 233, 233);
	border-radius: 4px;
	box-shadow: 0 0 10px 0px rgb(230, 230, 230);
	/* overflow: hidden; */
	background: white;
}

.title-container {
	position: sticky;
	top: 0;
	padding-top: 1em;
	box-shadow: 0 6px 4px -4px grey;
	background: white;
	border-radius: 3px;
	overflow: hidden;
}

.title {
	font-weight: 700;
	margin-bottom: 1em;
}

.comment {
	border-radius: 3px;
	box-shadow: 0 0 1px 0px grey inset;
	/* background: white; */
}

.list-main-container {
	flex: 1;
	margin-top: 0.5em;
}

.list-main-item {
	display: flex;
	flex-direction: column;
	border: none;
	border-radius: 3px;
	box-shadow: 0 0 1px 0px grey inset;
	margin-top: 0.4em;
	padding: 0.2em 0.8em;
}

.list-main-item>*{
	min-height: 2em;
}

.list-content {
	display: flex;
	justify-content: center;
	align-items: center;
	text-align: center;
	margin: 0 0.8em;
	white-space: pre-line;
	word-break: break-all;
}

</style>
