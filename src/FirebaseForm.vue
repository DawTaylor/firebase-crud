<template>
	<div class="container column">	
		<h2 class="title is-1">Adicionar novo lembrete</h2>
		<form>
			<label for="nome">Lembrete:</label>
			<p class="control">
				<input type="text" class="input" :class="{ 'is-danger' : this.errors.nome, 'is-success' : !this.errors.nome }" v-model="lembrete.nome" placeholder="Nome" @keydown="validar">
			</p>
			<label for="nome">Descrição:</label>
			<p class="control">
				<textarea class="textarea" :class="{ 'is-danger' : this.errors.descricao, 'is-success' : !this.errors.descricao }" v-model="lembrete.descricao" placeholder="Sobrenome" @keydown="validar"></textarea>
			</p>
			<button @click="cadastrar" type="button" class="button is-primary is-large">Cadastrar</button>
			<button type="reset" class="button is-danger is-large">Limpar</button>
		</form>
		<div class="modal" :class="{ 'is-active' : this.errors.show }">
			<div class="modal-background"></div>
			<div class="modal-content">
			    <article class="message is-danger">
				  <div class="message-header">
				    ATENÇÃO!
				  </div>
				  <div class="message-body">
				    Um ou mais campos não foram informados corretamente.
				  </div>
				</article>
			</div>
			<button class="modal-close" @click="fechaAlerta"></button>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return  {
				lembrete : {
					nome : '',
					descricao : ''
				},
				errors : {
					nome : false,
					descricao : false
				}
			}
		},
		methods : {
			validar() {
				this.errors.nome = (!this.lembrete.nome)
				this.errors.descricao = (!this.lembrete.descricao)

				return (this.errors.nome || this.errors.descricao)
			},
			cadastrar() {
				console.log("Validação", this.validar())
				if(!this.validar()){
					firebase.database().ref('lembretes/').push(this.lembrete).then(() => {
						this.lembrete.nome = ''
						this.lembrete.descricao = ''
					})
				} else {
					this.errors.show = true
				}
			},
			fechaAlerta() {
				this.errors.show = false
			}
		},
		created() {
			this.validar()
		}
	}
</script>