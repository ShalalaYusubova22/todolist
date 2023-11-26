<template>
    <div class="notes">
        <div class="container">
            <div class="notes-nav">
                <h2 v-if="search.length === 0">{{ notes.length ? 'Все заметки' : 'Нет заметок' }}</h2>
                <h2 v-if="search && notes.length > 0">Поиск...</h2>
                <h2 v-if="search && notes.length === 0">Ничего не найдено...</h2>
                <button @click="grid = !grid">
                    <img src="@/assets/img/grid.svg" alt="" v-if="grid">
                    <img src="@/assets/img/list.svg" alt="" v-else>
                    <span>{{ grid ? 'Сетка' : 'Список' }}</span>
                </button>
            </div>
            <transition-group tag="div" class="notes-grid" name="notes" :class="{column: grid}">
                <NoteItem 
                v-for="(note, index) in notes"
                :key="index"
                :note="note"
                @deleteNote="$emit('deleteNote', note.id)"
                @changeNote="$emit('changeNote', note.id)"
            />
            </transition-group>
        </div>
    </div>
</template>
<script>
import NoteItem from './NoteItem.vue'
export default {
  props: ['notes', 'search'],
  components: { NoteItem },
  data() {
    return {
        grid: false
    }
  },
    
}
</script>
<style>
    
</style>