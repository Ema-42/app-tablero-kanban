<script setup>
import { reactive } from "vue";
import InputNew from "./InputNew.vue";
const boards = reactive([
  {
    id: crypto.randomUUID(),
    name: "Tablero 1",
    items: [
      {
        id: crypto.randomUUID(),
        title: "Nota 1",
      },
      {
        id: crypto.randomUUID(),
        title: "Nota 2",
      },
    ],
  },
  {
    id: crypto.randomUUID(),
    name: "Tablero 2",
    items: [
      {
        id: crypto.randomUUID(),
        title: "Nota 3",
      },
      {
        id: crypto.randomUUID(),
        title: "Nota 4",
      },
    ],
  },
]);
const handleNewItem = (text, board) => {
  board.items.push({
    id: crypto.randomUUID(),
    title: text.value,
  });
};
const handleNewBoard = () => {
  const name = prompt("Nombre del Tablero: ");
  if (!!name) {
    boards.push({
      id: crypto.randomUUID(),
      name: name,
      items: [],
    });
  }
};
const startDrag = (event, board, item) => {
  event.dataTransfer.setData(
    "text/plain",
    JSON.stringify({ boardId: board.id, itemId: item.id })
  );
};
const onDrop = (event, dest) => {
  const { boardId, itemId } = JSON.parse(
    event.dataTransfer.getData("text/plain")
  );
  const originBoard = boards.find((board) => board.id === boardId);
  const originItem = originBoard.items.find((item) => item.id === itemId);
  dest.items.push({ ...originItem });
  originBoard.items = originBoard.items.filter((item) => item !== originItem);
};
</script>

<template>
  <nav>
    <ul>
      <button class="btn-crear-tablero" @click.prevent="handleNewBoard">Crear un tablero </button>
      
    </ul>
  </nav>
  <div class="boards-container">
    <div class="boards">
      <div
        class="board"
        @drop="onDrop($event, board)"
        @dragover.prevent
        @dragenter.prevent
        v-for="board in boards"
        :key="board.id"
      >
        <div class="nombre-tablero">
          {{ board.name }}
        </div>
        <InputNew @onNewItem="(text) => handleNewItem(text, board)"></InputNew>
        <div class="items">
          <div
            class="item"
            draggable="true"
            @dragstart="startDrag($event, board, item)"
            v-for="item in board.items"
            :key="item.id"
          >
            {{ item.title }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

nav ul{
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;

}

nav ul a {
  display: block;
  padding: 10px;
  text-decoration: none;
}
a {
  color: #efefef;
  font-weight: bold;
}
.boards {
  display: flex;
  gap: 10px;
}
.board {
  background-color: #efefef;
  padding: 1rem;
  border-radius: 10px;
  color: black;
}
.item {
  background-color: #a2ecb2;
  padding: 10px;
  border-radius: 5px;
}
.items {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.btn-crear-tablero{
  padding: 0.7rem;
  font-size: 18px;
  width: 100%;
  background-color: #2b4d3d;
  outline: none;
  border: none;
  border-radius: 10px;
  margin-bottom: 2rem;
  cursor: pointer;
}
.btn-crear-tablero:hover{
  background-color: #345d4a;
}
.nombre-tablero{
  text-align: center;
  padding-top: 0.5rem;
  padding-bottom: 2rem;
  font-size: 18px;
  font-weight: bold;
  text-transform: capitalize;
}
</style>
