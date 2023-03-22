<template>
		<div v-if="avatar" class="bluesky-avatar">
			<img :src="avatar"/>
			<div v-if="record" class="bluesky-did">
				<p>{{ record.data.records[0].uri.split('/',3)[2] }}</p>
			</div>
			<div v-if="record" class="bluesky-record">
				<li v-for="i in record.data.records">
					<p><span class="name">{{ id }}</span></p>
					<p><span class="text">{{ i.value.text }}</span></p>
					<p><span class="time"><a :href="i.uri">{{ i.value.createdAt }}</a></span></p>
				</li>
			</div>
		</div>
</template>

<script>
import axios from 'axios'
let default_id="syui.syui.ai";

export default {
	data () {
		return {
			id: null,
			record: null,
			avatar: "https://at.syui.ai/image/1gNGwD6W74qb_Nuncr5H5i9UADEtdyds9myxRGnkGMw/rs:fill:1000:1000:1:0/plain/bafkreibxgpwttqvpsnn5yrvqkx47nwuzpzrkfyladqy2hbj3chedph3fni@jpeg",
		}
	},
	mounted() {
		axios.get('https://syui.ai/xrpc/com.atproto.repo.listRecords?user=syui.syui.ai&collection=app.bsky.feed.post')
			.then(response => (this.record = response))
			.catch(error => console.log(error))
			this.id = "@" + default_id;
	}
}
</script>

<style>
div#app {
	list-style: none;
	margin: 100px;
}
.bluesky-avatar img {
	width: 55px;
}
span.time {
	color: blue;
}
span.name {
	font-weight: 700;
	background-color: #a3c3ff1a;
	padding:10px;
}
span.text {
    font-weight: 400;
    font-size: 19px;
}
.bluesky-record li {
	border-bottom: solid 1px #ccc;
}
.bluesky-record p {
	padding:0 20px 0;
}
.bluesky-record {
	border: solid 1px #ccc;
	border-radius: 10px;
	margin: 50px 100px 0 0;
}
a {
	color: #00A4E1;
	font-weight: '700';
}
footer#footer {
	text-align: center;
}
span.text {
	word-break: break-all;
}
p.tl-avatar img {
    width: 20px;
}
code {
    font-size: 15px;
				/*color: #3f89ff;*/
    padding: 5px 5px 5px 5px;
    background-color: #d4deee2b;
}
li {
list-style-type: none; 
}
@media screen and (max-width:1000px) { 
	div#app{list-style:none;margin:0px}.bluesky-avatar img{width:55px}span.time{color:#00f}span.name{background-color:rgba(163,195,255,.10196078431372549);padding:10px}.bluesky-record li{border-bottom:1px solid #ccc}.bluesky-record p{padding:0 20px 0}.bluesky-record{border:1px solid #ccc;border-radius:10px;margin:0px 0px 0 0}a{color:#3f89ff}footer#footer{text-align:center}
	span.text {
		word-break: break-all;
	}
}
</style>
