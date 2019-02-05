<template>
    <div id="_modal_container"  v-show="modal_visibility" @click.stop="closeModel">
        <div id="_modal_content" :class="size +' '+ type" @click.stop="">
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
            },
            type:{
                default: "info"
            }
        },
        model: {
            prop: 'visibility',
            event: 'click'
        },

        data() {
            return {
                modal_visibility: this.visibility,
                modal_size: this.size,
                modal_type: this.type,
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
        transition: width 2s;
        -webkit-transition: width 2s; /* Safari 3.1 to 6.0 */
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
        box-shadow: 0px 24px 48px rgba(0, 0, 0, 0.2);
        transition: 0.3s;
        left: 20%;
        position: fixed; /* Stay in place */
        z-index: 1; /* Sit on top */
        padding: 10px; /* Location of the box */
        background-color: #fefefe;
        border: 1px solid rgba(136, 136, 136, 0.47);
        width: 60%;
    }

    #_modal_dismiss_container {
        text-align: right;
        margin-top: 10px;
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

    .error{
        box-shadow: 0px 10px 30px rgba(216, 0, 12, 0.25) !important;
    }
    .success{
        box-shadow: 0px 10px 30px rgba(79, 138, 16, 0.25) !important;
    }
    .warning{
        box-shadow: 0px 10px 30px rgba(159, 96, 0, 0.25) !important;
    }
    .info{
        box-shadow: 0px 10px 30px rgba(0, 82, 155, 0.25) !important;
    }
</style>
