<template>
    <div class="inputBox shadow" v-on:keyup.enter="addTodo">
        <input type="text" v-model="newTodoItem">
        <span class="addContainer" v-on:click="addTodo">
            <i class="fa-solid fa-plus addBtn"></i>
        </span>
        <AlertModal v-if="showModal" @close="showModal = false">
            <h3 slot="header">
                경고!
                <button class="modal-default-button" @click="showModal = false">
                    OK
                </button>
            </h3>
            <div slot="body">아무것도 입력하지 않으셨습니다.</div>
        </AlertModal>
    </div>
</template>

<script>
import AlertModal from './common/AlertModal.vue';
export default {

    data: function () {
        return {
            newTodoItem: "",
            showModal: false,
        }
    },

    mounted() {

    },

    methods: {
        addTodo() {
            if (this.newTodoItem !== '') {
                // this.$emit('addTodoItem', this.newTodoItem)
                this.$store.commit('addOneItem',this.newTodoItem);
                this.clearInput();
            } else {
                this.showModal = !this.showModal;
            }
        },
        clearInput() {
            this.newTodoItem = '';
        },
        closeModal() {
            this.showModal = false;
        },

    },
    components: {
       AlertModal,
    },
};
</script>
<style scoped>
input:focus {
    outline: none;
}

.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}

.inputBox input {
    border-style: none;
    font-size: 0.9rem;
}

.addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}

.addBtn {
    color: white;
    vertical-align: middle;
}

.closeModalBtn {
    color: #42b983;
}
</style>