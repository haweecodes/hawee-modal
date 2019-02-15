<template>
<div class="_modal_container" v-show="MVisibility" @click.stop="closeModel">
    <div class="_modal_content" ref="modal_content" :class="[size, type]" @click.stop="" role="dialog">
        <slot></slot>
        <div class="_modal_dismiss_container">
            <button class="_modal_dismiss button" @click="closeModel">Close</button>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: "Modal",

    props: {
        visibility: {
            type: Boolean,
            required: true
        },
        size: {
            default: "small"
        },
        type: {
            default: "info"
        }
    },
    model: {
        prop: "visibility",
        event: "click"
    },

    data() {
        return {
            MVisibility: this.visibility,
            MSize: this.size,
            MType: this.type
        };
    },
    methods: {
        closeModel(event) {
            this.$refs.modal_content.classList.add("out")
            setTimeout(() => {
                this.MVisibility = false;
                event.stopPropagation();
                this.$emit("click", false);
                this.$refs.modal_content.classList.remove("out")
            }, 400);

        }
    },
    watch: {
        visibility() {
            this.MVisibility = this.visibility;
        }
    }
};
</script>

<style>
*,
*:before,
*:after {
    box-sizing: border-box;
}

._main_container p {
    margin: 0;
}

._modal_container {
    transition: width 2s;
    -webkit-transition: width 2s;
    /* Safari 3.1 to 6.0 */
    position: fixed;
    /* Stay in place */
    z-index: 1;
    /* Sit on top */
    padding-top: 100px;
    /* Location of the box */
    left: 0;
    top: 0;
    width: 100%;
    /* Full width */
    height: 100%;
    /* Full height */
    overflow: auto;
    /* Enable scroll if needed */
    background-color: rgb(0, 0, 0);
    /* Fallback color */
    background-color: rgba(0, 0, 0, 0.4);

}

._modal_content {
    box-shadow: 0px 24px 48px rgba(0, 0, 0, 0.2);
    transition: 0.3s;
    left: 20%;
    position: fixed;
    /* Stay in place */
    z-index: 1;
    /* Sit on top */
    padding: 10px;
    /* Location of the box */
    background-color: #fefefe;
    border: 1px solid rgba(136, 136, 136, 0.47);
    width: 60%;
    animation-name: zoom-in;
    animation-duration: 0.6s;
}

.out {
    animation-name: zoom-out;
    animation-duration: 0.6s;
}

@-webkit-keyframes zoom-in {
    from {
        -webkit-transform: scale(1)
    }

    to {
        -webkit-transform: scale(2)
    }
}

@keyframes zoom-in {
    from {
        transform: scale(0.4)
    }

    to {
        transform: scale(1)
    }
}

@-webkit-keyframes zoom-out {
    from {
        -webkit-transform: scale(1)
    }

    to {
        -webkit-transform: scale(2)
    }
}

@keyframes zoom-out {
    from {
        transform: scale(1)
    }

    to {
        transform: scale(0)
    }
}

@media only screen and (max-width: 600px) {
    ._modal_content {
        max-height: 60%;
        overflow-y: scroll;
    }
}

._modal_dismiss_container {
    text-align: right;
    margin-top: 10px;
}

.button {
    background-color: #4caf50;
    /* Green */
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
}

.small {
    left: 30% !important;
    width: 35% !important;
}

.medium {
    left: 25% !important;
    width: 45% !important;
}

.large {
    left: 20% !important;
    width: 60% !important;
}

.error {
    box-shadow: 0px 10px 30px rgba(216, 0, 12, 0.25) !important;
}

.success {
    box-shadow: 0px 10px 30px rgba(79, 138, 16, 0.25) !important;
}

.warning {
    box-shadow: 0px 10px 30px rgba(159, 96, 0, 0.25) !important;
}

.info {
    box-shadow: 0px 10px 30px rgba(0, 82, 155, 0.25) !important;
}
</style>
