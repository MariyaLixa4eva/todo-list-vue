<template>
    <emoji-picker @select="onSelectEmoji"/>
</template>

<script>
import EmojiPicker from 'vue3-emoji-picker'
import 'vue3-emoji-picker/css'

export default {
    components: {
        EmojiPicker,
    },
    methods: {
        onSelectEmoji(emoji) {
            let piker = emoji.i;
            this.$emit('add-emoji', piker);
            }
        },
    };
</script>