<template>
  <div class="containier">
    <app-header></app-header>
    <div class="mail-box">
      <app-slidebar :messages="messages"></app-slidebar>
      <app-content :messages="messages"></app-content>
    </div>
  </div> 
</template>

<script>
  import Header from './Header.vue'
  import Slidebar from './Slidebar.vue'
  import Content from './Content.vue'
  import messages from './data/messages'
  import randomMessages from './data/random-messages'
  import { eventBus } from './main'

  export default {
    data() {
      return {
        messages: messages
      }
    },

    created() {
      eventBus.$on('sentMessage', (data) => {
        let temp = [data.message];
        this.messages = temp.concat(this.messages.slice(0));
      });

      eventBus.$on('refreshMessages',()=>{
        let randomIndex = Math.floor(Math.random() * randomMessages.length);
        let temp = [randomMessages[randomIndex]];
        this.messages = temp.concat(this.messages.slice(0));
      })
    },

    components: {
      appHeader: Header,
      appSlidebar: Slidebar,
      appContent: Content
    },

    
  }
</script>