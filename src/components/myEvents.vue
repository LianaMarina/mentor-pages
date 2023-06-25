<template>
  <div class="events" v-if="events.length>0">
    <my-event
        v-for="event in events"
        :event="event"
        :key="event.id"
        @deleteEvent="$emit('deleteEvent', event)"
        :enterVisible="enterVisible"
    >
    </my-event>
  </div>
  <div class="" v-else>Мероприятий нет</div>
</template>

<script>
import myEvent from "@/components/myEvent";
export default {
  components: {myEvent},
  props: {
    events: {
      type: Array,
      required: true,
    },
    enterVisible: {
      type: Boolean,
      required: true,
      default: true,
    }
  }
}
</script>

<style scoped>

</style>
