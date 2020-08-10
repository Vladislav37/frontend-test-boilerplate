<template>
    <transition name ="modal">
        <div class=wrapWin >
            <div class="headerModalWindow"></div>
                <h3>{{modalWindowTitle}}</h3>
                <span>
                    <i
                            class="material-icons"
                            @click="closeWindow"
                    >
                        close
                    </i>
                </span>
            <div class="contentModalWindow">
                <slot></slot>
            </div>
            <div class="footerModalWindow">
                <button
                        type="button"
                        @click="addRow"
                >
                    {{titleButton}}
                </button>
            </div>
        </div>
    </transition>
</template>

<script>
    export default {
        name: "ModalVue",
        props: {
            modalWindowTitle: {
                type: String,
                default: 'Окно информации'
            },
            titleButton: {
                type: String,
                default: 'Ок',
            },
        },
        data: () => ({

        }),
        methods: {
            closeWindow () {
                this.$emit('closeModalWindow');
            },
            addRow () {
                this.$emit('addRecordFromModalWindow');
            },
        }
    }
</script>

<style scoped>
    i {
        cursor: pointer;
    }

</style>