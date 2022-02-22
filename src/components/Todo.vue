<template>
   <div class="w-[450px] h-[600px] p-[10px] bg-[white] flex flex-col rounded-md overflow-auto">
    <!-- To do input start -->
     <div class="inline-flex justify-center">  
         <input class="w-[300px] h-[50px] outline-0 border-solid border-2 border-[#444F60]" type="text" name="todo" v-model="newToDo" 
         @keyup.enter="addTask">
         <button class="w-[80px] h-[50px] bg-[#444F60] text-white" @click="addTask">Ekle</button>
      </div>
    <!-- To do input end -->
    <!-- To do list start -->
    <div class="w-full h-auto">
       <ul>
    <li class="w-full h-auto inline-flex justify-between h-auto bg-red-100 my-1 p-[5px]" 
    :class="{'bg-green-400': todo.isComplate}"
    v-for="(todo, index) in toDoList" :key="index">
        <div class="w-[300px] h-auto bg-red break-words">
        {{todo.toDoItem}}
      </div>
       <div class="flex flex-col">
        <!-- Delet button start -->
          <button class="w-[90px] h-auto bg-[#444F60] text-white mb-px" @click="deleteToDoItem(index)">
            Sil
        </button>
        <!-- Delet button end -->
          <button class="w-[90px] h-auto bg-[#444F60] text-white" @click="itemComplete(index)">Tamamlandı</button>
       </div>
    </li>
  </ul>
      
    </div>
  <!-- To do list end -->
   </div>
</template>

<script setup>

  import { ref, reactive} from 'vue'

  // New To do input Start
  let newToDo = ref('');
  //New To do input End

  // To do list start 
  const toDoList = reactive([]).reverse();
  // To do list end 

  // Add new to do item start
  const addTask = () => {
    if(newToDo.value != ''){
      toDoList.unshift({
      toDoItem: newToDo.value,
      isComplate: false,
    });
    newToDo.value = '';
    }
  } 
  // Add new to do item end

  // Delet to do item start 
  const deleteToDoItem = ( index ) => toDoList.splice(index, 1);
  // Delet to do item end
  
   const itemComplete = ( index ) => {
    toDoList[index].isComplate = !toDoList[index].isComplate 
   }
</script>