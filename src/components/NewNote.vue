<template>
    <div class="new-note">
        <label>Title</label>
        <input v-model="note.title" type="text">
        <label>Priority</label>
        <select v-model="note.priority" style="margin-bottom: 20px">
            <option v-for="(option, index) in note.options"
                    :value="option"
                    :key="index"
            >
                {{ option }}
            </option>
        </select>
        <label>Description</label>
        <textarea v-model="note.descr"></textarea>
        <label></label>
        <button class="btn btnPrimary" @click="addNote">New note</button>
    </div>
</template>

<script>
    export default {
        props: {
            note: {
                type: Object,
                required: true
            }
        },
        methods: {
            addNote () {
                this.$emit('addNote', this.note)
            }
        }
    }
</script>

<style lang="scss">
    .new-note {
        text-align: center;
    }
</style>