<template>
    <div class="index-background">
        <div
            mx-auto
            max-w-62.4996rem
            py-1.1256rem
            px-0.75rem
            h-full
            flex
            flex-col
            justify-between
        >
            <div class="index-scroll">
                <div class="text-#8280FF font-bold text-1.1256rem">
                    Chat-HuiJutong 2.0
                </div>
                <div
                    v-for="message in messageList"
                    :key="message.id"
                    mb-1.1256rem
                >
                    <div
                        :class="
                            message.type === 'USER' ? 'index-message-right' : ''
                        "
                    >
                        <div
                            class="text-#999999 text-0.75rem mb-0.3756rem"
                            v-if="message.type === 'AI'"
                        >
                            Presented By Chat-HuiJutong 2.0
                        </div>
                        <div flex>
                            <div
                                class="index-message"
                                :class="
                                    message.type === 'USER'
                                        ? 'index-message-user'
                                        : 'index-message-ai'
                                "
                            >
                                {{ message.value }}
                            </div>
                        </div>

                        <div class="text-#bbace8 text-0.75rem mt-0.3756rem">
                            {{ message.time }}
                        </div>
                    </div>
                </div>
            </div>
            <div flex flex-col items-center>
                <div w-full class="index-input">
                    <div flex>
                        <textarea
                            v-model="text"
                            @input="autoHeight"
                            class="w-94% b-0"
                            :maxlength="1000"
                        >
                        </textarea>
                        <div
                            class="w-6% text-right cursor-pointer"
                            @click="sendMessage"
                        >
                            发送
                        </div>
                    </div>
                    <div class="mt-0.3756rem text-#5B5B5B">
                        {{ text.length }} / 4000
                    </div>
                </div>
                <div class="text-0.8748rem mt-0.9996rem text-#C2C2C2">
                    Copyright @ 2022-2023 荟聚通All Rights Reserved
                </div>
            </div>
        </div>
    </div>
</template>
<script setup lang="ts">
const messageList = reactive([
    { id: 0, time: '05/28-11:30', value: '你好', type: 'USER' },
    { id: 1, time: '05.28-11:30', value: '你好', type: 'AI' },
])
const text = ref('')

const autoHeight = () => {
    const textareaVal = document.querySelector('textarea') as HTMLElement
    textareaVal.style.height = 'auto'
    textareaVal.style.height = textareaVal.scrollHeight + 'px'
}
const sendMessage = () => {
    if (text.value) {
        messageList.push({
            id: messageList.length,
            time: '05/28-11:30',
            value: text.value,
            type: 'USER',
        })
        text.value = ''
    }
    nextTick(() => {
        autoHeight()
        document.querySelector('.index-scroll')!.scrollTop =
            document.querySelector('.index-scroll')!.scrollHeight
    })
}
</script>

<style scoped>
:deep(.arco-textarea-wrapper) {
    border-radius: 0.5004rem;
}
.index-message-right {
    display: flex;
    align-items: flex-end;
    flex-direction: column;
}
.index-background {
    height: 100vh;
    background: linear-gradient(
        135deg,
        #f0e7f9 0%,
        #f4f0ff 36%,
        #fff5fb 57%,
        #ecdedf 100%
    );
}
.index-logo {
    font-size: 1.5rem;
    font-weight: bold;

    color: rgba(130, 128, 255, 0.71);
}
.index-alert {
    font-size: 0.8748rem;
    font-weight: normal;
    color: rgba(0, 0, 0, 0.24);
}
.index-input {
    min-height: 5.6256rem;
    width: 100%;
    padding: 0.9996rem;
    margin-bottom: 0.75rem;
    background: #ffffff;
    box-shadow: 0rem 0.2496rem 0.6252rem 0rem rgba(0, 0, 0, 0.06);
    border: 0;
    border-radius: 0.6876rem;
}

.index-message-user {
    color: #fff;
    background: #bbace8;
}
.index-message-ai {
    color: #24272d;
    background: #ffffff;
}
.index-message {
    padding: 0.8748rem;
    border-radius: 0.75rem;
    box-shadow: 0rem 0.2496rem 0.6252rem 0rem rgba(0, 0, 0, 0.06);
}

.index-scroll {
    overflow: scroll;
    -ms-overflow-style: none; /* IE and Edge */
    scrollbar-width: none;
}
.index-scroll::-webkit-scrollbar {
    display: none;
}
</style>
