<template>
    <transition name ="modal">
        <div class="modal-window-mask">
            <div class="wrap-window">
                <div class="container-window">
                    <div class="header-modal-window">
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
                    <div class="content-modal-window">
                        <slot></slot>
                    </div>
                    <div class="footer-modal-window">
                        <button
                            class="modal-window-button"
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
        data: function() {
            return {};
        },
        methods: {
            closeWindow() {
                this.$emit('closeModalWindow');
            },
            addRow() {
                this.$emit('addRecordFromModalWindow');
            },
        }
    }
</script>

<style scoped>
.modal-window-mask {
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

.wrap-window {
    display: table-cell;
    vertical-align: middle;
}

.container-window {
    width: 300px;
    margin: 0px auto;
    /*padding: 20px 30px;*/
    background-color: #fff;
    border-radius: 2px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
    transition: all 0.3s ease;
    font-family: Helvetica, Arial, sans-serif;
}

.header-modal-window {
    padding: 0px 5px 0 5px;
    margin-top: 0;
    background-color: #42b983;
    color: #fff;
    overflow: hidden;
}

.header-modal-window h3 {
    float: left;
}

.header-modal-window span {
    right: 0px;
}

.modal-window-button {
    color: #fff;
    background: #42b983;
    border: 0;
    border-radius: 8px;
    padding: 10px 20px;
    cursor: pointer;
}

.modal-window-button:hover {
    background: #3DB4B2;
}

i {
    cursor: pointer;
}

</style>