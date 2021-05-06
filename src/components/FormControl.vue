<template>
    <input 
        type="text"
        class="text-input form-control form-control-lg"
        v-model="scanned"
        @keyup.enter="submitScan"
        :enabled="enabled"
    />
</template>

<script>

export default({
    name: 'FormControl',
    props : {
        enabled : String
    },
    data(){
        return {
            scanned: '',
            step: 1
        }
    },
    methods: {
        submitScan(){
            this.$emit('submit-action',this)
            this.scanned = ''
        }
    }
})

</script>

<style scoped>
    .text-input{
		border: none !important;
		border-bottom: 5px solid #dad9d9 !important;
		border-radius: 0 !important;
		font-size: 50px;
		text-align: center;
	}

	.text-input:focus{
		border: none !important;
		box-shadow: none !important;
		border-bottom: 5px solid #62d4e0 !important;
	}	

	.form-control::-webkit-input-placeholder{
		color: #dddddd !important;
		font-size: 70px !important;
		font-style: oblique !important;
	}
</style>