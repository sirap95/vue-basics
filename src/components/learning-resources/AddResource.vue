<template>
    <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
        <template #default>
            <p>Unfortunately at least one input value is invalid </p>
            <p>Please check all the input field and ensure that you entered
                 a value in all the input fields </p>
        </template>
        <template #actions>
            <base-button @click="confirmError">OK</base-button>
        </template>
    </base-dialog>
    <base-card>
        <form @submit.prevent="submitData">
            <div class="form-control">
                <label for="title">Title</label>
                <input type="text" name="title" id="title" ref="titleInput">
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea id="description" name="description" rows="3" ref="descInput"> </textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input type="text" name="link" id="link" ref="linkInput">
            </div>
            <div class="form-control">
                <base-button @click="storeData" type="submit">Add resource</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>
export default {
    inject: ['addResources'],
    data() {
        return {
            inputIsInvalid: false
        }
    },
    methods: {
        storeData() {
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDescr = this.$refs.descInput.value;
            const enteredLink = this.$refs.linkInput.value;

            if (enteredTitle.trim() === '' || enteredDescr.trim() === '' || enteredLink.trim() === '') {
                this.inputIsInvalid = true;
                return;
            }

            this.addResources(enteredTitle, enteredDescr, enteredLink);
        },
        confirmError() {
            this.inputIsInvalid = false
        }
    }
}
</script>

<style scoped>
label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
}

input,
textarea {
    display: block;
    width: 100%;
    font: inherit;
    padding: 0.15rem;
    border: 1px solid #ccc;
}

input:focus,
textarea:focus {
    outline: none;
    border-color: #3a0061;
    background-color: #f7ebff;
}

.form-control {
    margin: 1rem 0;
}
</style>