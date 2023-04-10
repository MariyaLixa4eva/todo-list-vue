<template>
    <div class="notes">
        <div class="note"
        v-for="(note, index) in notes"
        :class="{full: !grid}"
        >
        <div class="note-header">
            <p>{{ note.title }}</p>
            <p style="cursor: pointer; color: #E86A33;" @click="removeNote(index)">x</p>
        </div>
        <div class="note-body">
            <p>{{ note.desc }}</p>
            <span>{{ note.date }}</span>
        </div>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        notes: {
        type: Array,
        required: true,
        },
        grid: {
        type: Boolean,
        required: true,
        },
    },
    methods: {
        removeNote(index) {
        this.$emit("remove", index);
        },
    },
    };
</script>

<style scoped>
    .notes {
        display: flex;
        justify-content: space-between;
        align-items: center;
        gap: 10px;
        flex-wrap: wrap;
        width: 90%;
        margin: 0 auto;
    }
    .note {
        background-color: #F2E3DB;
        border: 2px solid #E86A33;
        width: 40%;
        border-radius: 15px;
        padding: 10px;
        transition: 0.25s;
    }
    .note:hover {
        box-shadow: 0 10px 10px rgba(0,0,0,0.2);
        transform: translate(0, -6px);
    }
    .full {
        width: 100%;
    }
    .note-header {
        color: #263A29;
        display: flex;
        justify-content: space-between;
    }
    .note-body {
        color: #41644A;
    }
    .note-body span {
        color: #999;
    }
    @media all and (max-width:500px) {
        .note {
        height: 220px;
        padding: 10px;
    }
    .full {
        height: 160px;
    }
}
</style>
