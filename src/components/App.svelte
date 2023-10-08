
 <script lang="ts">
  import { text } from "svelte/internal";
	import Lista from "./lista.svelte";
	interface listaProps {
		name:string;
		readonly id:number;
		description:string;
		readonly date:Date;
	}
	export let tarefas:listaProps[] = JSON.parse(localStorage.getItem("@listagem_tarefas"));
	if(!tarefas) {
		tarefas = [];
	}
	function adicionarTarefa() {
		let name =  document.querySelector("#name") as HTMLInputElement;;
		let description =  document.querySelector("#description") as HTMLInputElement;;
		if(!name.value || !description.value) return;
		let data = {
			name:name.value,
			description:description.value,
			id:Math.floor(Math.random() * 5000),
			date:new Date(),
		}
		tarefas.push(data);
		localStorage.setItem("@listagem_tarefas", JSON.stringify(tarefas));
		tarefas = tarefas;
	}
	function deleteTarefa(id:number) {
		let index = tarefas.indexOf(tarefas.find(function(tarefa){return tarefa.id == id}));
		tarefas.splice(index,1);
		tarefas = tarefas;
		localStorage.setItem("@listagem_tarefas", JSON.stringify(tarefas));
	}
	function editarTarefa(id:number) {
		let tarefa = tarefas.find(function(tarefa){return tarefa.id ==id});
		let textArea = document.getElementById(`textArea-${id}`) as HTMLInputElement;
		let btn= document.getElementById(`editbtn-${id}`) as HTMLInputElement;
		let tarefaDescription =  document.getElementById(`tarefa_description-${id}`) as HTMLInputElement;
		tarefa.description = textArea.value;
		textArea.style.display = "none";
		btn.style.display = "none";
		tarefaDescription.style.display = "initial";
		tarefas = tarefas;
		localStorage.setItem("@listagem_tarefas", JSON.stringify(tarefas));
	}
   </script>
	
<main>
<div class="container justify-content-center">
	<h1 style="text-align:center">Lista De Tarefas</h1>
	<div class="container justify-content-center" style="width:50%;margin-top:40px">
		<div class="input-group mb-3">
			<input id="name" type="text" class="form-control" placeholder="Nome da tarefa" aria-label="Recipient's username" aria-describedby="button-addon2">
			<input id="description" type="text" class="form-control" placeholder="Descrição da tarefa" aria-label="Recipient's username" aria-describedby="button-addon2">

			<button on:click={adicionarTarefa} class="btn btn-outline-secondary" type="button" id="button-addon2">Adicionar</button>
		  </div>
		<ul class="list-group">
			{#each tarefas as tarefa}
				<Lista editFunc={editarTarefa} deleteFunc={deleteTarefa} id="{tarefa.id}" name="{tarefa.name}" description="{tarefa.description}"> </Lista>
			{/each}
			
		  </ul>
	</div>
</div>

</main>




<style>
	:global(body){
		background-color: black;
		font-weight: bolder;
	}
	:root{
		--cor-fundo:#555;
	}
	main {
		margin-top:150px;
	}


.scroll {
  width: 60px;
  height: 60px;
  border: 2px solid #333;
  border-radius: 50%;
  display: inline-block;
  margin: 0 auto;
  margin-top:50px;
  margin-bottom:30px;
  justify-content: center;
  animation: down 1.5s infinite;
  -webkit-animation: down 1.5s infinite;
}

.scroll::before {
  content: "";
  position: absolute;
  top: 15px;
  left: 18px;
  width: 18px;
  height: 18px;
  border-left: 2px solid #333;
  border-bottom: 2px solid #333;
  transform: rotate(-45deg);
}
.list-group {
	max-height: 250px;
	overflow-y: auto;
}
@keyframes down {
  0% {
    transform: translate(0);
  }
  20% {
    transform: translateY(15px);
  }
  40% {
    transform: translate(0);
  }
}
@-webkit-keyframes down {
  0% {
    transform: translate(0);
  }
  20% {
    transform: translateY(15px);
  }
  40% {
    transform: translate(0);
  }
}
</style>
