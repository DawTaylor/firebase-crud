<template>
	<div class="container column">	
		<h2 class="title is-1">Não esquecer de:</h2>
		<div class="box" v-for="lembrete in lembretes">
		  <article class="media">
		    <div class="media-content">
		      <div class="content">
		        <p>
		          <strong v-text="lembrete.nome"></strong>
		          <br>
		          <span v-text="lembrete.descricao"></span>
		        </p>
		      </div>
		      <nav class="level-right">
		        <div class="level">
		          <a class="level-item" @click="editLembrete(lembrete)">
		            <span class="icon is-small"><i class="fa fa-pencil"></i></span>
		          </a>
		          <a class="level-item" @click="delLembrete(lembrete)">
		            <span class="icon is-small"><i class="fa fa-trash"></i></span>
		          </a>
		        </div>
		      </nav>
		    </div>
		  </article>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return  {
				lembretes : []
			}
		},
		methods : {
			getLembretes() {
				let lembretes = firebase.database().ref('lembretes')

				lembretes.on('value', (snapshot) => {
					this.lembretes = []
					snapshot.forEach(data => {
						let lembrete = data.val()
						lembrete.key = data.key
						this.lembretes.push(lembrete)
					})
				})
			},
			delLembrete(lembrete) {
				let ref = firebase.database().ref('lembretes')
				ref.child(lembrete.key).remove()
			},
			editLembrete(lembrete) {
				Event.$emit('editar', { 'lembrete' : lembrete })
			}
		},
		created() {
			this.getLembretes()
		}
	}
</script>