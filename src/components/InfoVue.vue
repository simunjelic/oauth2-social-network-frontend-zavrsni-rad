<template>
    <div class="alert alert-success" role="alert">
    {{info}}
  </div>
</template>

<script>
    export default{
        name: 'InfoMsg',
        props: ['info']
    }
</script>