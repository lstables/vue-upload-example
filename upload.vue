<template>

    <div>
        <small>Change/Upload</small>
        <input type="file" @change="onFileChange">
        <button class="btn btn-success btn-xs" @click="upload">Upload</button>
    </div>

</template>

<script>
    export default {

        props: ['any_props'],

        data() {
            return {
                image: '',
                file: null
            }
        },

        methods: {
            onFileChange(e) {
                let files = e.target.files || e.dataTransfer.files;
                if (!files.length)
                    return;
                this.createImage(files[0]);
            },
            createImage(file) {
                let reader = new FileReader();
                let vm = this;
                reader.onload = (e) => {
                    vm.image = e.target.result;
                };
                reader.readAsDataURL(file);
            },
            upload(){
                axios.post('/path/to/url', {image: this.image}).then(response => {
                    alert('Uploaded');
                });
            }
        }

    }
</script>
<style>
/* any styles */

</style>