<template>

</template>

<script>
export default {
  data () {
    return {
      quickReplies: [
        {
          'button_type': 'postback',
          'order_index': 1,
          'title': '☝️ Actualiser',
          'payload': 'I will send first',
          'is_loop': false
        },
        {
          'button_type': 'postback',
          'order_index': 1,
          'title': '☝️ Information Bus',
          'payload': 'I will send two',
          'is_loop': true
        },
        {
          'button_type': 'postback',
          'order_index': 2,
          'title': 'Mes alertes',
          'payload': 'I will send 3',
          'is_loop': false
        },
        {
          'button_type': 'postback',
          'order_index': 2,
          'title': 'Mes alertesR',
          'payload': 'I will send 3',
          'is_loop': false
        }
      ]

    }
  }
}
</script>

<style>

</style>
