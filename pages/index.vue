<template>

</template>

<script>
export default {
  middleware: [
    function ({redirect}) {
      redirect('/page/1');
    },
  ]
}
</script>
