<template>
    <nav class="navbar navbar-dark bg-dark mb-2">
        <div class="container-fluid">
            <div class="col">
                <a class="navbar-brand" href="#">
                    <img src="@/assets/brand_logo.svg" class="float-start">
                </a>
                <span class='navbar-text text-light d-print-none float-start'> &nbsp; {{ title }} </span>
            </div>
        </div>
    </nav>
</template>

<script>
export default({
    props: {
        title: String
    }
})
</script>
