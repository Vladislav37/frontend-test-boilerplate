<template>
    <div class="mySelect">
        <p
                class="titleSelect"
                @click="visibleOptions = !visibleOptions"
        >{{selected}}</p>
        <div
                class="option"
                v-if="visibleOptions"
        >
            <p
                v-for="option in options"
                :key="option.id"
                @click="selectOption(option)"
            >
                {{option.name}}
            </p>
        </div>
    </div>
</template>

<script>
    export default {
        name: "SelectForModalWindow",
        props: {
            options: {
                type: Array,
                default() {
                    return [];
                }
            },
            selected: {
                type: String,
                default: ''
            }
        },
        data: () =>({
            visibleOptions: false,
        }),
        methods: {
            selectOption (option) {
                this.$emit('select', option);
                this.visibleOptions = false;
            }
        },
    }
</script>

<style>
    .mySelect {
        position: relative;
        width: 150px;
    }

    .titleSelect {
        border: solid 1px #aeaeae;
        cursor: pointer;
    }

    p {
        margin: 0;
    }

    .option {
        border: solid 1px #aeaeae;
        position: absolute;
        top: 20px;
        right: 0;
        width: 100%;
    }

    .option p:hover {
        background: #e7e7e7;
    }

</style>