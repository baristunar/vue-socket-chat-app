
<template>
  <chat-section :messageList="messageList" />
</template>

<script>
import chatSection from "./components/chatSection.vue";

export default {
  components: {
    chatSection,
  },
  data() {
    return {
      

      messageList: [
        
      ],
    };
  },
};
</script>

