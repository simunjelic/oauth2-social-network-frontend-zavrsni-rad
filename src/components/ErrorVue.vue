<template>
    <div class="alert alert-danger" role="alert">
    {{error}}
  </div>
</template>

<script>
    export default{
        name: 'ErrorMsg',
        props: ['error']
    }
</script>