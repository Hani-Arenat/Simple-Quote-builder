<template>
    <div class="parent">
        <div class="divv">
          <slot></slot>
        </div>
    </div>
    
</template>

<script>
export default {


}
</script>

<style scoped>
    .divv {
        border: 2px solid #3F51B5;
        border-radius: 5px;
        float: left;
        margin: 5px;
        padding: 5px;
    }
    .parent {
        display: inline-block;
    }
</style>
