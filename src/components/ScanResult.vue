<template>
    <div class="mt-3">
        <div v-if="!result" class="alert alert-warning">
            <b>Error</b> : {{ message }}
        </div>
    </div>
    <div v-if="eval == 'good'" class="mt-3">
        <div  class="alert alert-success">
            <i class="fas fa-check"></i><b> Scanning Success</b>
        </div>
    </div>
    <div v-if="eval == 'bad'" class="mt-3">
        <div class="alert alert-danger">
            <i class="fas fa-times"></i><b> Scanning complete - ERROR RECORDED</b>
        </div>
    </div>
</template>

<script>
export default({
    props: {
        message: String,
        result: Boolean,
        eval: String
    }
})
</script>