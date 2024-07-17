<template>
  <div class="fixed top-0 left-0 right-0 bottom-0 flex justify-center items-center">
    <div class="w-8/12 h-full overflow-y-auto bg-gray-100 p-4 rounded-lg shadow-lg">
      <!-- 聊天历史 -->
      <div class="flex-grow overflow-y-auto p-4 bg-gray-100">
        <div v-for="message in messages" :key="message.id" class="mb-4">
          <div v-if="message.user === 'bot'" class="flex items-start">
            <!-- <img :src="botAvatar" alt="Bot Avatar" class="w-10 h-10 rounded-full mr-2"> -->
            <div class="bg-gray-200 text-gray-700 rounded-lg p-2">
              {{ message.text }}
            </div>
          </div>
          <div v-else class="flex items-start justify-end">
            <div class="bg-blue-500 text-white rounded-lg p-2">
              {{ message.text }}
            </div>
            <!-- <img :src="userAvatar" alt="User Avatar" class="w-10 h-10 rounded-full ml-2"> -->
          </div>
        </div>
        <!-- 消息列表 -->
      </div>
    </div>
    <!-- 独立的输入区域容器 -->
    <div class="fixed bottom-0 left-0 right-0 bg-white border-t border-gray-200 flex items-center justify-between px-4 py-2">
      <!-- 下拉列表 -->
      <div class="flex space-x-2">
        <!-- 下拉菜单 -->
        <select v-model="selectedOption1" class="border rounded-lg p-2">
          <option v-for="option in options1" :key="option.value" :value="option.value">
            {{ option.text }}
          </option>
        </select>
        <select v-model="selectedOption2" class="border rounded-lg p-2">
          <option v-for="option in options2" :key="option.value" :value="option.value">
            {{ option.text }}
          </option>
        </select>
      </div>
      <!-- 发送按钮 -->
      <button @click="sendMessage" class="bg-blue-500 text-white py-2 px-4 rounded-lg">Send</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const messages = ref([
  {
    id: 1,
    user: 'bot',
    text: 'Hello! How can I assist you today?'
  },
  {
    id: 2,
    user: 'user',
    text: 'Can you help me with coding questions?'
  },
  {
    id: 3,
    user: 'bot',
    text: 'Of course! I can help with various programming topics.'
  }
]);

const selectedOption1 = ref('');
const selectedOption2 = ref('');
const options1 = ref([
  { value: 'option1', text: 'Option 1' },
  { value: 'option2', text: 'Option 2' },
  { value: 'option3', text: 'Option 3' }
]);
const options2 = ref([
  { value: 'optionA', text: 'Option A' },
  { value: 'optionB', text: 'Option B' },
  { value: 'optionC', text: 'Option C' }
]);

const botAvatar = '/path/to/bot-avatar.jpg';
const userAvatar = '/path/to/user-avatar.jpg';

const sendMessage = () => {
  if (selectedOption1.value && selectedOption2.value) {
    messages.value.push({
      id: messages.value.length + 1,
      user: 'user',
      text: `${selectedOption1.value} ${selectedOption2.value}`
    });
    selectedOption1.value = '';
    selectedOption2.value = '';
  }
};
</script>
