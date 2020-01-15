<template>
	
	<modal-layouts name="viewRecord">
		
		<template slot="heading">Information sur l'étudiant</template>

		<template slot="main">
			<table class="table">
				<thead>
					<tr class="text-center">
						<th>ID</th>
						<th>Matricule</th>
						<th>Nom et Prenom</th>
						<th>Email</th>						
					</tr>
				</thead>
				<tbody>
					<tr class="text-center">
						<th v-text="viewRec.id"></th>
						<td v-text="viewRec.phone"></td>
						<td v-text="viewRec.name"></td>
						<td v-text="viewRec.email"></td>						
					</tr>
				</tbody>
			</table>
		</template>

		<template slot="footer">
			<button type="button" class="btn btn-outline-secondary" data-dismiss="modal">Fermer</button>
		</template>

	</modal-layouts>

</template>

<script>
	import ModalLayouts from '../partials/ModalLayouts'

	export default {
		props: ['viewRec'],

		components: { ModalLayouts }
	};
</script>