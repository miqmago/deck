<!--
  - SPDX-FileCopyrightText: 2018 Nextcloud GmbH and Nextcloud contributors
  - SPDX-License-Identifier: AGPL-3.0-or-later
-->

<template>
	<div v-if="card" class="card-menu" @click.stop.prevent>
		<NcButton v-if="card.referenceData"
			type="tertiary"
			:title="t('deck','Open link')"
			@click="openLink">
			<template #icon>
				<LinkIcon :size="20" />
			</template>
		</NcButton>
		<NcActions>
			<CardMenuEntries :card="card" @edit-title="editTitle" />
		</NcActions>
	</div>
</template>
<script>
import { NcActions, NcButton } from '@nextcloud/vue'
import LinkIcon from 'vue-material-design-icons/Link.vue'
import CardMenuEntries from './CardMenuEntries.vue'

export default {
	name: 'CardMenu',
	components: { NcActions, NcButton, LinkIcon, CardMenuEntries },
	props: {
		card: {
			type: Object,
			default: null,
		},
	},
	emits: ['edit-title'],
	methods: {
		openLink() {
			window.open(this.card?.referenceData?.openGraphObject?.link)
			return false
		},
		editTitle(id) {
			this.$emit('edit-title', id)
		},
	},
}
</script>
