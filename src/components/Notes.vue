<template xmlns: xmlns:>
    <div class="notes">
        <div class="note" :class="{full: !grid}" v-for="(note, index) in notes" :key="index">
            <div class="note-header" :class="{full: !grid}">
                <p v-if="note.priority == 'standard'" class="standard">
                    {{ note.title }}
                </p>
                <p v-else-if="note.priority == 'important'" class="important">
                    {{ note.title }}
                </p>
                <p v-else-if="note.priority == 'very important'" class="very_important">
                    {{ note.title }}
                </p>
                <!--another method:-->
                <!--<p :style="`color: ${note.color}`"></p>-->
                <p style="cursor: pointer" @click="removeNote(index)">x</p>
            </div>
            <div class="note-body">
                <p>{{ note.descr }}</p>
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
                required: true
            },
            grid: {
                type: Boolean,
                required: true
            }
        },
        methods: {
            removeNote (index) {
                this.$emit('remove', index)
                console.log(`Note id - ${index} removed!`)
            }
        }
    }
</script>

<style lang="scss">
    .notes {
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-wrap: wrap;
        padding: 40px 0px;
    }
    .note {
        width: 48%;
        padding: 18px 20px;
        margin-bottom: 20px;
        background-color: #ffffff;
        transition: all .25s cubic-bezier(.02,.01,.47,1);
        box-shadow: 0 30px 30px rgba(0,0,0,.02);
        &:hover {
            box-shadow: 0 30px 30px rgba(0,0,0,.04);
            transform: translate(0, -6px);
            transition-delay: 0s !important;
        }
        &.full {
            width: 100%;
            text-align: center;
        }
    }
    .note-header {
        display: flex;
        align-items: center;
        justify-content: space-between;
        h1 {
            font-size: 32px;
        }
        p {
            font-size: 22px;
        }
        p.standard {
            color: #0000FF;
        }
        p.important {
            color: #FFCC00;
        }
        p.very_important {
            color:#FF0000;
        }
        svg {
            margin-right: 12px;
            color: #999999;
            &.active {
                color: #0000FF
            }
            &:last-child {
                margin-right: 12px;
            }
        }
        &.full {
            justify-content: center;
            p {
                margin-right: 16px;
                &.last-child {
                    margin-right: 0px;
                }
            }
        }
    }
    .note-body {
        p {
            margin: 20px 0;
        }
        span {
            font-size: 14px;
            color: #999999;
        }
    }
</style>
