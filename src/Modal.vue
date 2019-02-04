<template>
    <div id="_modal_container"  v-show="modal_visibility" @click.stop="closeModel">
        <div id="_modal_content" :class="size" @click.stop="">
            <slot></slot>
            <div id="_modal_dismiss_container">
                <button id="_modal_dismiss" @click="closeModel">Close</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Modal',

        props: {
            visibility: {
                type: Boolean,
                required: true
            },
            size:{
                default: "small"
            }
        },
        model: {
            prop: 'visibility',
            event: 'click'
        },

        data() {
            return {
                modal_visibility: this.visibility,
                modal_size: this.size
            }
        },
        methods: {
            closeModel(event) {
                this.modal_visibility = false
                event.stopPropagation()
                this.$emit('click', false)
            }
        },
        watch: {
            visibility() {
                this.modal_visibility = this.visibility
            },
        }
    }
</script>

<style>
    *, *:before, *:after {
        box-sizing: border-box;
    }

    #_main_container p {
        margin: 0;
    }

    #_modal_container {
        position: fixed; /* Stay in place */
        z-index: 1; /* Sit on top */
        padding-top: 100px; /* Location of the box */
        left: 0;
        top: 0;
        width: 100%; /* Full width */
        height: 100%; /* Full height */
        overflow: auto; /* Enable scroll if needed */
        background-color: rgb(0, 0, 0); /* Fallback color */
        background-color: rgba(0, 0, 0, 0.4);
    }

    #_modal_content {
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
        transition: 0.3s;
        left: 20%;
        position: fixed; /* Stay in place */
        z-index: 1; /* Sit on top */
        padding: 10px; /* Location of the box */
        background-color: #fefefe;
        border: 1px solid #888;
        width: 60%;
    }

    #_modal_dismiss_container {
        text-align: right;
    }

    .small{
        left: 30% !important;
        width: 35% !important;
    }
    .medium{
        left: 25% !important;
        width: 45% !important;
    }
    .large{
        left: 20% !important;
        width: 60% !important;
    }
</style>
