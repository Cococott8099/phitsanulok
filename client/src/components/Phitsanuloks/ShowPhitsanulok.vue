<template>
	<div>
		<h1>สถานที่ท่องเที่ยวพิษณุโลก</h1>
		<!-- <p>id: {{ phitsanulok.id }}</p> -->
		<p>สถานที่ : {{ phitsanulok.title }}</p>
		<!-- <p>content: {{ phitsanulok.content }}</p> -->
		<p>ประวัติ : {{ phitsanulok.category }}</p>
		<!-- <p>status: {{ phitsanulok.status }}</p> -->
		<p>
			<button v-on:click="navigateTo('/phitsanulok/edit/' + phitsanulok.id)">
				แก้ไข
			</button>
			<button v-on:click="navigateTo('/phitsanuloks')">กลับ</button>
		</p>
	</div>
</template>
<script>
import PhitsanuloksService from "@/services/PhitsanuloksService";
export default {
	data() {
		return {
			phitsanulok: null,
		};
	},
	async created() {
		try {
			let phitsanulokId = this.$route.params.phitsanulokId;
			this.phitsanulok = (await PhitsanuloksService.show(phitsanulokId)).data;
		} catch (error) {
			console.log(error);
		}
	},
	methods: {
		navigateTo(route) {
			this.$router.push(route);
		},
	},
};
</script>
<style scoped>
</style>
