<template>
  <div>
    <p>{{con}}</p>
  </div>
</template>

<script>
export default {
    emits: ['shout-out'],
    data(){
        return {
            con: 'Thanks'
        }
    },
}
</script>

<style>

</style>