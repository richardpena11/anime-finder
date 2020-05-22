<template>
  <div class="error_container">
        <div class="error_status">
            {{ error.status }}
        </div>

        <div class="error_message">
            {{ error.message }}
        </div>
  </div>
</template>

<script>
export default {
    props:[
        "error"
    ],
}
</script>

<style>

    .error_container{
        text-align: center;
        margin-top: 50px;
    }

    .error_status{
        font-size: 150px;
        font-weight: 700;
    }

    .error_message{
        font-size: 40px;
        font-weight: 700;
    }
</style>