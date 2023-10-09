<script lang="ts">
    export let name:string
    export let description:string
    export let id:number
    export let deleteFunc:Function
    export let editFunc:Function
    export let checked:boolean
    export let doneTarefa:Function
    function expand(id:number) {
        let icon =  document.getElementById(`expand_${id}`) as HTMLInputElement;
        if(icon.className == "fa-solid fa-caret-down") {
            icon.setAttribute("class","fa-solid fa-caret-right");
        }else {
            icon.setAttribute("class","fa-solid fa-caret-down");
        }
        
    }
    function editarTarefa(id:number) {
    let spanDescription = document.getElementById(`tarefa_description-${id}`) as HTMLInputElement;
    let spanDescriptionTextArea = document.getElementById(`textArea-${id}`) as HTMLInputElement;
    let editBtn = document.getElementById(`editbtn-${id}`) as HTMLInputElement;
    spanDescription.style.display = "none";
    spanDescriptionTextArea.style.display = "";
    editBtn.style.display = "";
	}
   </script>


{#if checked == true}
<li  class="list-group-item">
    <input id="checkbox-{id}" on:change={doneTarefa(id)}  style="float:left;margin-top:5px;height:15px;width:15px;margin-right:5px;" type="checkbox" {checked}/>
    <i on:click={deleteFunc(id)} id="tarefa_delete" style="float:left;margin-top:4px;margin-right:10px;" class="fa-solid fa-trash-can"></i>
    <div on:click={expand(id)} style="width:100%" data-bs-toggle="collapse" href="#tarefaCollapse-{id}" class="tarefa-{id} pointer"  >
         <a href="#{id}"  role="button" aria-expanded="false" aria-controls="collapseExample">
        <span style="text-decoration: line-through;" id="Tarefa-name-{id}" >{name}</span> 
        <i style="float:right;margin-top:3px;font-size:17px" id="expand_{id}"  class="fa-solid fa-caret-right"></i>
    </a>
</div>
   
    <div class="tarefas_card_body" ></div>
    <div class="collapse" id="tarefaCollapse-{id}">
        <div class="tarefas_card">
         <p id="tarefa_description-{id}"><span>{description}</span><i on:click={editarTarefa(id)} id="tarefa_edit" style="float:right;margin-top:5px" class="fa-solid fa-pencil"></i></p>
         <textarea id="textArea-{id}" style="width:100%;height:100%;display:none">{description}</textarea>
         <a on:click={editFunc(id)} style="display:none;" id="editbtn-{id}" class="editbtn" >Atualizar</a>
        </div>
       
      </div>
</li>
{:else if checked == false}
<li  class="list-group-item">
    <input id="checkbox-{id}" on:change={doneTarefa(id)}  style="float:left;margin-top:5px;height:15px;width:15px;margin-right:5px;" type="checkbox"/>
    <i on:click={deleteFunc(id)} id="tarefa_delete" style="float:left;margin-top:4px;margin-right:10px;" class="fa-solid fa-trash-can"></i>
    <div on:click={expand(id)} style="width:100%" data-bs-toggle="collapse" href="#tarefaCollapse-{id}" class="tarefa-{id} pointer"  >
         <a href="#{id}"  role="button" aria-expanded="false" aria-controls="collapseExample">
        <span id="Tarefa-name-{id}" >{name}</span> 
        <i style="float:right;margin-top:3px;font-size:17px" id="expand_{id}"   class="fa-solid fa-caret-right"></i>
    </a>
</div>
   
    <div class="tarefas_card_body" ></div>
    <div class="collapse" id="tarefaCollapse-{id}">
        <div class="tarefas_card">
         <p id="tarefa_description-{id}"><span>{description}</span><i on:click={editarTarefa(id)} id="tarefa_edit" style="float:right;margin-top:5px" class="fa-solid fa-pencil"></i></p>
         <textarea id="textArea-{id}" style="width:100%;height:100%;display:none">{description}</textarea>
         <a on:click={editFunc(id)} style="display:none;" id="editbtn-{id}" class="editbtn" >Atualizar</a>
        </div>
       
      </div>
</li>
{/if}



<style>
.list-group-item {
    color:white;
    background-color: #0f1421;
    -webkit-box-shadow: 7px 7px 15px -3px rgba(0,0,0,0.44);
    -moz-box-shadow: 7px 7px 15px -3px rgba(0,0,0,0.44);
    box-shadow: 7px 7px 15px -3px rgba(0,0,0,0.44);
}
.unvisible {
    display:none;
}
.visible {
    display:initial;
}
.list-group-item:hover{
    background-color: #151c2d;
}
a {
    width:100%;
	color:white;
	text-decoration: none;
}
a:hover {
	text-decoration: none;
}
.editbtn {
    padding:8px;
    background-color: #059464;
    color:white;
    border-radius:5px;
}
.editbtn:hover {
    background-color: #10ba81;
    cursor:pointer;
}
a span {
    text-align: center;
}
#tarefa_edit:hover {
    color:#72da9f;
    cursor:pointer;
}
#tarefa_delete:hover {
    color:	#da7272;
    cursor:pointer;
}
.tarefas_card {
	padding:10px;
	background-color: #1c233495;
	border-radius:5px;
	margin-top:5px;
	text-align:center;
}
.pointer:hover{
    cursor:pointer;
}
</style>
