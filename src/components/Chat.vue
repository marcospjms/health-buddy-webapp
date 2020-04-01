<template>
  <div class="webchat-container">
    <div
      id="webchat"
      @click="updateOpenStatus()"
    />
  </div>
</template>

<script>
import * as WebChat from '../assets/js/bot.js';
import { mapGetters } from 'vuex';
export default {
  props: {
    isOpen: {
      type: Boolean,
      default: false,
    },
  },
    computed: {
      ...mapGetters([
        'getLanguage',
      ]),
      initialPayload() { return `hello ${this.getLanguage || 'en'}`; },
    },
    watch: {
      getLanguage() {
        console.log(this.getLanguage);
        this.sendInitial();
      },
    },
    mounted() {
      this.setupChat();
      this.updateOpenStatus();
    },
    methods: {
      isMobile() {
        return false;
      },
      sendInitial() {
        WebChat.send(this.initialPayload);
      },
      updateOpenStatus() {
        setTimeout(() => {  
          if (WebChat.isOpen() === this.isOpen) return;
          this.$emit('update:isOpen', WebChat.isOpen()); 
        }, 100);
      },
      setupChat() {
        WebChat.default.init({
          selector: '#webchat',
          initPayload: this.initalPayload,
          channelUuid: 'f2cc9ec6-07f1-407a-8948-ece57761d88e',
          host: 'https://rapidpro.ilhasoft.mobi',
          title: 'HealthBuddy',
          hideWhenNotConnected: false,
          inputTextFieldHint: "Type a question...",
          profileAvatar: require('@/assets/img/doctor-darker.png'),
          openLauncherImage: require('@/assets/img/doctor-square.png'),
          disableTooltips: !this.isMobile(),
          docViewer: true,
          showFullScreenButton: true,
          params: {
            images: {
              dims: {
                width: 712,
                height: 844
              }
            },
            storage: "session"
          }
      });
    }
  }
}
</script>

<style lang="css">
    .launcher {
    -webkit-box-shadow: 1px 1px 5px 1px rgba(28,171,226,1);
    -moz-box-shadow: 1px 1px 5px 1px rgba(28,171,226,1);
    box-shadow: 1px 1px 5px 1px rgba(28,171,226,1);
    height: 8vh;
    width: 8vh;
  }

  .launcher:after {
    content: '';
    width: 8vh;
    height: 8vh;
    border: 4px solid #1CABE2;
    border-radius: 50%;
    position: absolute;
    animation: pulsate infinite 1.4s;
  }

  @-webkit-keyframes pulsate {
    0% {
      -webkit-transform: scale(1.1, 1.1);
      opacity: 1;
    }
    100% {
      -webkit-transform: scale(1.2, 1.2);
      opacity: 0;
    }
  }

  .conversation-container .close-button {
    display: flex;
    justify-content: center;
    align-items: center;

    display: inline-block;
    background-color: #1CABE2;
    border: 0;
    width: 40px;
    cursor: pointer;
  }

  .close-button:focus, .close-button:active, .close-button:hover {
    outline: none;
  }

  .close-button::-moz-focus-inner {
    border:0;
  }

  .conversation-container .close {
    display: inline-block;
    width: 20px;
    height: 20px;
  }

  .messages-container {
    min-height: 75vh;
  }

  @media only screen and (max-height: 500px) {
    .messages-container {
      min-height: 20vh;
    }
  }

  .conversation-container {
    max-height: 90vh;
  }

  .hide-sm {
    display: none;
  }

  .quickReplies-container {
    max-width: 100%;
  }

  .replies {
    align-items: stretch;
    padding: 0 0 0 0;
    overflow: auto;
    max-width: 100%;
    display:flex;
    flex-wrap:wrap;
  }

  .new-message {
    font-weight: bolder;
  }

  .send-icon {
    filter: brightness(50%);
  }

  .replies {
    justify-content: center;
  }

  .conversation-container .reply {
    width: 55%;
    min-width: 280px;
  }

  .avatar {
    min-width: 17px;
  }

  .message.with-avatar {
    background: white;
  }

  .title.with-avatar {
    color: white;
  }
</style>