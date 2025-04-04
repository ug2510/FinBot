<template>
  <div class="chat-container">
    <div class="chat-messages" ref="messagesContainer">
      <div
        v-for="(message, index) in messages"
        :key="index"
        :class="message.sender === 'user' ? 'user-message' : 'bot-message'"
        :style="{
          backgroundColor: darkMode
            ? message.sender === 'user'
              ? '#00796b'
              : '#424242'
            : message.sender === 'user'
              ? '#e0f7fa'
              : '#f0f0f0',
          color: darkMode ? 'white' : 'black',
        }"
      >
        {{ message.text }}
      </div>
    </div>

    <div class="chat-input-wrapper">
      <div
        class="chat-input"
        :style="{
          backgroundColor: darkMode ? '#333' : 'white',
          color: darkMode ? 'white' : 'black',
        }"
      >
        <q-input
          bottom-slots
          v-model="inputText"
          placeholder="Type a message..."
          @keyup.enter="sendMessage"
          :dark="darkMode"
          dense
          borderless
          autogrow
        >
          <template v-slot:prepend>
            <q-icon name="message" />
          </template>
        </q-input>
        <q-btn icon="send" @click="sendMessage" class="send-btn" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    darkMode: {
      type: Boolean,
      default: false,
    },
    leftDrawerOpen: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      inputText: '',
      messages: [],
    }
  },
  methods: {
    sendMessage() {
      if (this.inputText.trim() !== '') {
        this.messages.unshift({ text: this.inputText, sender: 'user' }) // Adds message to the top
        this.$nextTick(() => {
          this.scrollToTop()
        })
        setTimeout(() => {
          this.messages.unshift({ text: `Response to: ${this.inputText}`, sender: 'bot' })
          this.$nextTick(() => {
            this.scrollToTop()
          })
        }, 500)
        this.inputText = ''
      }
    },
    scrollToTop() {
      const container = this.$refs.messagesContainer
      container.scrollTop = 0
    },
  },
}
</script>

<style scoped>
.chat-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 85vh;
  width: 50%;
  padding: 16px;
  box-sizing: border-box;
  margin: auto;
}

.chat-messages {
  flex-grow: 1;
  overflow-y: scroll;
  padding: 16px;
  display: flex;
  flex-direction: column-reverse;
  align-items: center;
  width: 100%;
  max-height: calc(100vh - 80px);
}

.chat-input-wrapper {
  display: flex;
  width: 100%;
  padding: 10px;
}

.chat-input {
  display: flex;
  flex-grow: 1;
  align-items: center;
  padding: 10px;
  border-radius: 10px;
}

.user-message,
.bot-message {
  max-width: 70%;
  min-width: 30%;
  text-align: left;
  padding: 10px;
  border-radius: 8px;
  margin: 6px 0;
  transition:
    background-color 0.3s ease,
    color 0.3s ease;
}

.user-message {
  align-self: flex-end;
}

.bot-message {
  align-self: flex-start;
}

.send-btn {
  margin-left: auto;
}

.chat-messages::-webkit-scrollbar {
  width: 8px;
}

.chat-messages::-webkit-scrollbar-track {
  background: transparent;
}

.chat-messages::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 4px;
}

.chat-messages::-webkit-scrollbar-thumb:hover {
  background: #555;
}

/* Dark mode specific scrollbar */
.dark-mode .chat-messages::-webkit-scrollbar-thumb {
  background: black;
}

.dark-mode .chat-messages::-webkit-scrollbar-thumb:hover {
  background: #333;
}

@media (max-width: 600px) {
  .user-message,
  .bot-message {
    max-width: 90%;
  }
  .chat-input-wrapper {
    width: 90%;
  }
}
</style>
