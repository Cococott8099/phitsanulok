<template>
	<div>
		<h2>Get all Phitsanuloks</h2>
		<p><button v-on:click="logout">ออกระบบ</button></p>
		<h4>สถานที่ท่องเที่ยวพิษณุโลก มี {{ phitsanuloks.length }} แห่ง</h4>
		<p><button v-on:click="navigateTo('/phitsanulok/create')">เพิ่มสถานที่</button></p>
		<div v-for="phitsanulok in phitsanuloks" v-bind:key="phitsanulok.id">
			<!-- <p>id: {{ phitsanulok.id }}</p> -->
			<p>ชื่อสถานที่ : {{ phitsanulok.title }}</p>
			<!-- <p>content: {{ phitsanulok.content }}</p> -->
			<p>รายละเอียดสถานที่ท่องเที่ยว : {{ phitsanulok.category }}</p>
			<!-- <p>status: {{ phitsanulok.status }}</p> -->
			<p>
				<button v-on:click="navigateTo('/phitsanulok/' + phitsanulok.id)">ดูรายละเอียด</button>
				<button v-on:click="navigateTo('/phitsanulok/edit/' + phitsanulok.id)">
					แก้ไขรายละเอียด
				</button>
				<button v-on:click="deletePhitsanulok(phitsanulok)">ลบสถานที่</button>
			</p>
			<hr />
		</div>
	</div>
</template>
<script>
import PhitsanuloksService from "@/services/PhitsanuloksService";
export default {
	data() {
		return {
			phitsanuloks: [],
		};
	},
	async created() {
		this.phitsanuloks = (await PhitsanuloksService.index()).data;
	},
	methods: {
		logout() {
			this.$store.dispatch("setToken", null);
			this.$store.dispatch("setBlog", null);
			this.$router.push({
				name: "login",
			});
		},
		navigateTo(route) {
			this.$router.push(route);
		},
		async deletePhitsanulok(phitsanulok) {
			let result = confirm("Want to delete?");
			if (result) {
				try {
					await PhitsanuloksService.delete(phitsanulok);
					this.refreshData();
					location.reload();
				} catch (err) {
					console.log(err);
				}
			}
		},
		async refreshData() {
			this.phitsanuloks = (await PhitsanuloksService.index()).data;
		},
	},
};
</script>
<style scoped>
</style>
