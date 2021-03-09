<template>
	<IonApp>
		<IonSplitPane content-id="main-content">
			<ion-menu side="end" content-id="main-content" type="push">
				<ion-content>
					<ion-header>
						<ion-toolbar>
							<ion-buttons slot="end">
								<ion-button color="medium">
									<ion-icon slot="start" :ios="settingsOutline" :md="settingsSharp"></ion-icon>
								</ion-button>
							</ion-buttons>
						</ion-toolbar>
					</ion-header>
					<div class="background-blur">
						<ion-list id="inbox-list">
							<ion-list-header>Evgeniy</ion-list-header>
							<ion-note color="light">laravelka@yandex.ru</ion-note>
		
							<ion-menu-toggle auto-hide="false" v-for="(p, i) in appPages" :key="i">
								<ion-item @click="selectedIndex = i" router-direction="root" :router-link="p.url" lines="none" detail="false" class="hydrated" :class="{ selected: selectedIndex === i }">
									<ion-icon slot="start" :ios="p.iosIcon" :md="p.mdIcon"></ion-icon>
									<ion-label>{{ p.title }}</ion-label>
								</ion-item>
							</ion-menu-toggle>
						</ion-list>
		
						<ion-list id="labels-list">
							<ion-list-header>Последние</ion-list-header>
		
							<ion-item v-for="(label, index) in labels" lines="none" :key="index">
								<ion-icon slot="start" :ios="imagesOutline" :md="imagesSharp"></ion-icon>
								<ion-label>{{ label }}</ion-label>
							</ion-item>
						</ion-list>
					</div>
				</ion-content>
			</ion-menu>
			<ion-router-outlet id="main-content"></ion-router-outlet>
		</IonSplitPane>
	</IonApp>
</template>

<script lang="ts">
import { IonApp, IonContent, IonIcon, IonItem, IonLabel, IonList, IonListHeader, IonMenu, IonMenuToggle, IonNote, IonRouterOutlet, IonSplitPane } from '@ionic/vue';
import { defineComponent, ref } from 'vue';
import { useRoute } from 'vue-router';
import { settingsOutline, settingsSharp, imagesOutline, imagesSharp, heartOutline, heartSharp, peopleOutline, peopleSharp, paperPlaneOutline, paperPlaneSharp, trashOutline, trashSharp, exitOutline, exitSharp } from 'ionicons/icons';

export default defineComponent({
	name: 'App',
	components: {
		IonApp, 
		IonContent, 
		IonIcon, 
		IonItem, 
		IonLabel, 
		IonList, 
		IonListHeader, 
		IonMenu, 
		IonMenuToggle, 
		IonNote, 
		IonRouterOutlet, 
		IonSplitPane,
	},
	setup() {
		const selectedIndex = ref(0);
		const appPages = [
			{
				title: 'Мой профиль',
				url: '/folder/Profile',
				iosIcon: peopleOutline,
				mdIcon: peopleSharp
			},
			{
				title: 'Сообщения',
				url: '/folder/Outbox',
				iosIcon: paperPlaneOutline,
				mdIcon: paperPlaneSharp
			},
			{
				title: 'Любимые',
				url: '/folder/Favorites',
				iosIcon: heartOutline,
				mdIcon: heartSharp
			},
			{
				title: 'Корзина',
				url: '/folder/Trash',
				iosIcon: trashOutline,
				mdIcon: trashSharp
			},
			{
				title: 'Выход',
				url: '/folder/Spam',
				iosIcon: exitOutline,
				mdIcon: exitSharp
			}
		];
		const labels = ['На рабочий стол', 'Приложение'];
		
		const path = window.location.pathname.split('folder/')[1];
		if (path !== undefined) {
			selectedIndex.value = appPages.findIndex(page => page.title.toLowerCase() === path.toLowerCase());
		}
		
		const route = useRoute();
		
		return { 
			selectedIndex,
			appPages, 
			labels,
			settingsOutline, 
			settingsSharp, 
			imagesOutline, 
			imagesSharp, 
			heartOutline, 
			heartSharp, 
			peopleOutline, 
			peopleSharp, 
			paperPlaneOutline, 
			paperPlaneSharp, 
			trashOutline, 
			trashSharp, 
			exitOutline, 
			exitSharp,
			isSelected: (url: string) => url === route.path ? 'selected' : ''
		}
	}
});
</script>

<style scoped>
	ion-menu ion-content {
		position: absolute;
		top: 0;
		--background: none;
		background-image: url(https://wallpaper.csplague.com/wp-content/uploads/2020/03/girly-sky-androidwallpapers-wallpapers-background.jpg);
		background-position: center top;
		background-repeat: no-repeat;
		background-size: cover;
	}

	.background-blur {
		background: rgba(255, 255, 255, 0.2);
		backdrop-filter: blur(10px);
		position: absolute;
		height: 100vh;
		padding: 0 4px;
		width: 100%;
		left: 0;
		top: 0;
	}

	ion-menu.md ion-content {
		--padding-start: 8px;
		--padding-end: 8px;
		--padding-top: 20px;
		--padding-bottom: 20px;
	}

	ion-menu.md ion-list {
		padding: 20px 0;
	}

	ion-menu.md ion-note {
		margin-bottom: 30px;
	}

	ion-menu.md ion-list-header,
	ion-menu.md ion-note {
		padding-left: 10px;
	}

	ion-menu.md ion-list#inbox-list {
		border-bottom: 1px solid var(--ion-color-step-150, rgba(0, 0, 0, 0.2));
	}

	ion-menu.md ion-list#inbox-list ion-list-header {
		font-size: 22px;
		font-weight: 600;

		--color: white;

		min-height: 20px;
	}

	ion-menu.md ion-list#labels-list ion-list-header {
		font-size: 16px;

		margin-bottom: 18px;

		--color: white;

		min-height: 26px;
	}

	ion-menu.md ion-item {
		--padding-start: 10px;
		--padding-end: 10px;
		border-radius: 4px;
	}

	ion-menu.md ion-item.selected {
		--background: rgb(0 0 0 / 10%)!important;
	}

	ion-menu.md ion-item.selected ion-icon {
		color: #d9afc8;
	}

	ion-menu.md ion-item ion-icon {
		color: rgb(234 219 228 / 70%);
	}

	ion-menu.md ion-item ion-label {
		--color: white;
		font-weight: 500;
	}

	ion-menu.md ion-item.selected ion-label {
		color: #d9afc8;
	}

	ion-menu.ios ion-content {
		--padding-bottom: 20px;
	}

	ion-menu.ios ion-list {
		padding: 20px 0 0 0;
	}

	ion-menu.ios ion-note {
		line-height: 24px;
		margin-bottom: 20px;
	}

	ion-menu.ios ion-item {
		--padding-start: 16px;
		--padding-end: 16px;
		--min-height: 50px;
	}

	ion-menu.ios ion-item.selected ion-icon {
		color: #d9afc8;
	}

	ion-menu.ios ion-item ion-icon {
		font-size: 24px;
		color: rgb(234 219 228 / 70%);
	}

	ion-menu.ios ion-item ion-label {
		--color: white;
	}

	ion-menu.ios ion-item.selected ion-label {
		color: #d9afc8;
	}


	ion-menu.ios ion-list#labels-list ion-list-header {
		--color: white;
		margin-bottom: 8px;
	}

	ion-menu.ios ion-list#inbox-list ion-list-header {
		--color: white;
	}

	ion-menu.ios ion-list-header,
	ion-menu.ios ion-note {
		padding-left: 16px;
		padding-right: 16px;
	}

	ion-menu.ios ion-note {
		margin-bottom: 8px;
	}

	ion-note {
		display: inline-block;
		font-size: 16px;

		color: var(--ion-color-medium-shade);
	}

	ion-item.selected {
		--color: #d9afc8;
	}

	ion-list {
		background: rgba(0, 0, 0, 0)!important;
	}

	ion-item {
		--background: rgba(0, 0, 0, 0.1)!important;
	}

	@media (prefers-color-scheme: light) {
		ion-item {
			--background: rgba(255, 255, 255, 0)!important;
		}
	}
</style>