<template>
    <div class="new-note">
        <label>Название</label>
        <input v-model="note.title" type="text">
        <label>Содержание</label>
        <textarea v-model="note.desc">
        </textarea>
        <button type="button" @click="showEmoji = !showEmoji">
        😃
        </button>
        <EmojiPiker
            v-show="showEmoji"
            @close="showEmoji = !showEmoji"
            @add-emoji="addEmoji"
        />
        <button @click="addNote">Добавить заметку</button>
    </div>
</template>

<script>
import EmojiPiker from './EmojiPiker.vue';
export default {
    components: {
        EmojiPiker
    },
    props: {
        note: {
            type: Object,
            required: true,
        }
    },
    data () {
    return {
        showEmoji: false,
    }
    },
    methods: {
        addNote() {
            this.$emit('addNote', this.note)//название в скобках может быть любое
        },
        addEmoji(piker) {
            this.note.desc += piker
        }
    }
}
</script>

<style scoped>
.new-note {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    color:#F2E3DB;
}
.new-note button {
    border-radius: 15px;
    padding: 10px 20px;
    background-color: #E86A33;
    border: 2px solid #F2E3DB;
    color: #F2E3DB;
}
.new-note input,
.new-note textarea {
    width: 90%;
    padding: 15px;
    border-radius: 15px;
    background-color: #F2E3DB;
    border: 2px solid #E86A33;
}
</style>