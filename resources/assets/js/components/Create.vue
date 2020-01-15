<template>
	
	<modal-layouts name="addRecord" id="addRecord" @keydown.esc="clearModal" @click.left="clearModal">
		
		<template slot="heading">Ajoute etudiant</template>

		<template slot="main">
             <div class="form-group">
				<label for="phone">Matricule</label>

				<input type="text" 
					   name="phone" 
					   id="phone" 
					   class="form-control" 
					   v-model="record.phone"
					   @keydown="delete errors.phone">

				<span v-if="errors.phone" class="text-danger">
					<small v-text="errors.phone[0]"></small>
				</span>
			</div>
			<div class="form-group">
				<label for="name">Nom & Prenom</label>

				<input type="text" 
					   name="name" 
					   id="name" 
					   class="form-control" 
					   v-model="record.name"
					   @keydown="delete errors.name">

				<span v-if="errors.name" class="text-danger">
					<small v-text="errors.name[0]"></small>
				</span>
			</div>

			<div class="form-group">
				<label for="email">E-mail</label>

				<input type="email" 
					   name="email" 
					   id="email" 
					   class="form-control" 
					   v-model="record.email" 
					   @keydown="delete errors.email">

				<span v-if="errors.email" class="text-danger">
					<small v-text="errors.email[0]"></small>
				</span>
			</div>

			
		</template>

		<template slot="footer">
			<button type="button" 
					class="btn btn-outline-secondary" 
					@click="clearModal" 
					data-dismiss="modal">Annuler</button>

			<button type="submit" class="btn btn-outline-primary" @click="saveRecord">Sauvegarder</button>
		</template>

	</modal-layouts>

</template>

<script>
	import ModalLayouts from '../partials/ModalLayouts'

	export default {
		data() {
			return {
				record: {},
				errors: [],
			}
		},

		components: { ModalLayouts },

		methods: {
			saveRecord() {
				axios.post('/phonebooks', this.record)
					.then(data => {
						this.$emit('recordAdded', data);

						toast({
						  type: 'success',
						  title: 'L étudiant a été bien ajouté!'
						})

						this.record = {};
						$('#addRecord').modal('hide');
					})
					.catch(error => this.errors = error.response.data.errors)
			},

			clearModal() {
				this.errors = [];
				this.record = {};
			}
		}
	};
</script>