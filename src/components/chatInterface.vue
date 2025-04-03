<template>
  <div class="chat-container">
    <div class="chat-messages">
      <div
        v-for="(message, index) in messages"
        :key="index"
        :class="message.sender === 'user' ? 'user-message' : 'bot-message'"
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
        this.messages.push({ text: this.inputText, sender: 'user' })
        setTimeout(() => {
          this.messages.push({ text: `Response to: ${this.inputText}`, sender: 'bot' })
        }, 500)
        this.inputText = ''
      }
    },
  },
}
</script>

<style scoped>
.chat-container {
  display: flex;
  flex-direction: column;
  height: 100%;
}

.chat-messages {
  flex-grow: 1;
  overflow-y: auto;
  padding: 16px;
}

.chat-input-wrapper {
  display: flex;
  position: fixed;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  width: 50%;
  padding: 10px;
  transition: background-color 0.3s ease;
}

.input-container {
  display: flex;
  align-items: center;
  width: 50%;
}

.chat-input {
  display: flex;
  flex-grow: 1;
  align-items: center;
  padding: 10px;
  border-radius: 10px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s ease;
}

.user-message {
  background-color: #e0f7fa;
  align-self: flex-end;
  align-items: center;
  border-radius: 8px;
  padding: 8px;
  width: 50%;
  margin-bottom: 8px;
}

.bot-message {
  background-color: #f0f0f0;
  align-self: flex-start;
  border-radius: 8px;
  align-items: center;
  padding: 8px;
  margin-bottom: 8px;
  width: 50%;
}

.send-btn {
  margin-left: auto;
}
</style>
