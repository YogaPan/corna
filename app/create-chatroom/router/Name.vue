<template>
 <div id="tutorial-container">

   <div id="middle-container">
     <div id="register-form">
       <h1>Create new Chatroom</h1>
       <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
       <input ref="room-name" class="input-big" v-model="roomName" type="text" placeholder="#room name" autofocus>
     </div>
   </div>

   <div id="next">
     <!-- <button id="next-button" class="button-trans" @click="nextStep">Next -></button> -->
     <router-link id="next-button" class="button-trans" tag="button" to="/members">
      Next ->
     </router-link>
   </div>

 </div>
</template>

<script>

export default {
  data() {
    return {
      errorMessage: ''
    }
  },
  computed: {
    roomName: {
      get() {
        return this.$store.state.roomName
      },
      set(value) {
        this.$store.commit('updateRoomName', value)
      }
    }
  },
  methods: {
    nextStep() {
      if (this.$store.state.roomName === '') {
        this.errorMessage = 'Please fill in your room name.'
        this.$refs['room-name'].focus()
      } else {
        document.location.href = '#members'
      }
    }
  }
}

</script>

<style lang="less">

@import "~styles/init.less";

#tutorial-container {
  height: 100%;
  width: 100%;

  display: flex;
  flex-direction: column;
  justify-content: stretch;
}

#middle-container {
  width: 100%;
  flex: 1 0 auto;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

#register-form {
  width: 80%;

  h1 { font-weight: 100; }
  input {
    width: 100%;
    margin-top: 10px;
  }
  .error-message {  margin-top: 15px; }
}

#next {
  width: 100%;
  flex: 0 0 150px;

  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}

#next-button {
  width: 130px;
}

</style>
