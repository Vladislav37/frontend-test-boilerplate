<template>
    <transition name ="modal">
        <div class="modalWindowMask">
            <div class=wrapWindow>
                <div class="containerWindow">
                    <div class="headerModalWindow">
                        <h3>{{modalWindowTitle}}</h3>
                        <span>
                            <i
                                    class="material-icons"
                                    @click="closeWindow"
                            >
                                close
                            </i>
                        </span>
                    </div>
                    <div class="contentModalWindow">
                        <slot></slot>
                    </div>
                    <div class="footerModalWindow">
                        <button
                                class="modalWindowButton"
                                type="button"
                                @click="addRow"
                        >
                            {{titleButton}}
                        </button>
                    </div>
                </div>
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
.modalWindowMask {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: table;
    transition: opacity 0.3s ease;
}

.wrapWindow {
    display: table-cell;
    vertical-align: middle;
}

.containerWindow {
    width: 300px;
    margin: 0px auto;
    /*padding: 20px 30px;*/
    background-color: #fff;
    border-radius: 2px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
    transition: all 0.3s ease;
    font-family: Helvetica, Arial, sans-serif;
}

.headerModalWindow {
    padding: 0px 5px 0 5px;
    margin-top: 0;
    background-color: #42b983;
    color: #fff;
    overflow: hidden;
}

.headerModalWindow h3 {
    float: left;
}

.headerModalWindow span {
    right: 0px;
}

.modalWindowButton {
    color: #fff;
    background: #42b983;
    border: 0;
    border-radius: 8px;
    padding: 10px 20px;
    cursor: pointer;
}

.modalWindowButton:hover {
    background: #3DB4B2;
}

i {
    cursor: pointer;
}

</style>