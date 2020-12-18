<template>
  <div>
    <div class="container">
      <div
        class="chat--app--container d-flex justify-content-between align-items-start"
      >
        <div class="card mr-10">
          <ul class="messages" ref="container">
          
            <li
              v-for="item in messageList"
              :key="item.id"
              :class="{ 'current-user': item.isActive }"
            >
              {{ item.msg }} <small>{{ item.currentTime }}</small>
            </li>
          </ul>
          <div
            class="text-container d-flex justify-content-start align-items-start"
          >
            <input
              placeholder="Kurs nasıl gidiyor? :)"
              v-model="newMessage"
              type="text"
              @keydown.enter="send()"
            />

            <button class="btn-primary" :disabled="isDisable" @click="send()">Gönder</button>
          </div>
        </div>
        <div class="card card-light w-40">
          <div class="card--header">
            <h3>Aktif Kullanıcılar</h3>
          </div>
          <div class="card--body">
            <div
              class="active-user-item d-flex justify-content-start align-items-center"
            >
              <div
                class="badge d-flex justify-content-center align-items-center mr-5"
              >
                GK
              </div>
              <div class="full_name">Gökhan Kandemir</div>
            </div>
            <div
              class="active-user-item d-flex justify-content-start align-items-center"
            >
              <div
                class="badge d-flex justify-content-center align-items-center mr-5"
              >
                BT
              </div>
              <div class="full_name">Barış Tunar</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["messageList"],
  data() {
    return {
      newMessage: "",
      userGk: true,
    };
  },
  methods: {
    send() {
      while(this.newMessage != ""){
        const currentTime = new Date();
      const currentHour = currentTime.getHours();
      const currentMinute = currentTime.getMinutes();

      if (this.userGk) {
        const user = {
          id: 1,
          userName: "Gökhan Kandemir",
          isActive: true,
          msg: this.newMessage,
          currentTime: currentMinute < 0 ? currentHour + ":0" + currentMinute : currentHour + ":" + currentMinute
        };
        this.messageList.push(user);
        this.newMessage = "";
        this.userGk = false;
      } else {
        const user = {
          id: 2,
          userName: "Barış Tunar",
          isActive: false,
          msg: this.newMessage,
          currentTime: currentMinute < 0 ? currentHour + ":0" + currentMinute : currentHour + ":" + currentMinute,
        };
        this.messageList.push(user);
        this.newMessage = "";
        this.userGk = true;
      }
      }
      
    },
    scrollToEnd() {
      let content = this.$refs.container;
      content.scrollTop = content.scrollHeight;
    },
  },
computed:{
  isDisable(){
    return this.newMessage=="" ? true : false
  }
},

  updated() {
    this.scrollToEnd();
  },
  mounted() {
    this.scrollToEnd();
  },
};
</script>