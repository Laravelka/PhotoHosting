<template>
	<ion-page>
		<ion-header>
			<ion-toolbar class="custom" color="dark">
	
				<ion-buttons slot="start">
					<ion-back-button color="medium"></ion-back-button>
				</ion-buttons>
				<ion-buttons slot="end">
					<ion-menu-button color="medium"></ion-menu-button>
				</ion-buttons>
			</ion-toolbar>
		</ion-header>
		
		<ion-content class="custom" :fullscreen="true">
			<div id="container">
				<h1 class="text-uppercase">
					<strong color="white">PhotoCloud</strong>
				</h1>
				<hr>
				<p class="ion-padding" style="hsla(0,0%,100%,.7)">
					Начните загружать изображения простым перетаскиванием в любое место окна прямо сейчас. Ограничение на размер изображения 4 MB. После загрузки, Вам будут доступны прямые ссылки, BB-коды и миниатюры.
				</p>
				<ion-input type="file"></ion-input>
				<ion-button shape="round"><ion-icon slot="start" :md="imagesSharp" :icon="imagesOutline"></ion-icon> Выбрать изображение</ion-button>
			</div>
		</ion-content>
	</ion-page>
</template>

<script lang="ts">
	import { 
		IonButtons, 
		IonContent, 
		IonHeader, 
		IonMenuButton, 
		IonPage, 
		// IonTitle, 
		IonToolbar 
	} from '@ionic/vue';
	import { defineComponent } from 'vue';
	import { imagesOutline, imagesSharp } from 'ionicons/icons';

	export default defineComponent({
		name: 'Folder',
		components: {
			IonButtons,
			IonContent,
			IonHeader,
			IonMenuButton,
			IonPage,
			//IonTitle,
			IonToolbar
		},
		setup() {
			return {
				imagesOutline,
				imagesSharp,
			};
		}
	});
</script>

<style scoped>
	#container {
		text-align: center;
		position: absolute;
		left: 0;
		right: 0;
		top: 40%;
		transform: translateY(-40%);
		background: rgba(0, 0, 0, 0.2);
		backdrop-filter: blur(8px);
		border-radius: 32px;
		padding: 8px 0px;
		margin: 0 8px;
	}

	#container strong {
		color: white;
		font-size: 2rem;
		line-height: 26px;
		text-transform: uppercase;
	}

	#container p {
		color: rgb(255 255 255 / 70%);
	}

	#container a {
		text-decoration: none;
	}

	ion-header ion-toolbar.custom {
		background: transparent!important;
		--background: transparent!important;
		--color: var(--ion-color-light);
		--ion-color-base: transparent!important;
	}

	ion-content {
		position: absolute;
		top: 0;
		--background: none;
		background-image: url(https://wallpaper.csplague.com/wp-content/uploads/2020/03/girly-sky-androidwallpapers-wallpapers-background.jpg);
		background-position: center top;
		background-repeat: no-repeat;
		background-size: cover;
	}

	.ios ion-toolbar {
		--color: var(--ion-color-light)!important;
	}

	hr {
		max-width: 100px;
		background: rgb(0 0 0 / 35%);
		height: 3px;
		border-radius: .35rem;
	}
</style>