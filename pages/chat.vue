<template>
    <div class="c-wrap">
        <div class="c-chat" ref="block">
            <Message 
                v-for="m in messages" :key="m.text"
                :name="m.name"
                :text="m.text"
                :owner="m.id === user.id"
            />
        </div>
        <div class="c-form">
            <ChatForm />
        </div>
    </div>
</template>

<script>
import Message from '@/components/Message';
import ChatForm from '@/components/ChatForm';
import {mapState} from "vuex"
export default {
    head() {
        return{
            title: `Комната ${this.user.room}`
        } 
    },
    middleware: ["chat"],
    components: {Message, ChatForm},
    computed: mapState(["user", "messages"]),
    watch:{
        messages(){
            setTimeout(() => {
                this.$refs.block.scrollTop = this.$refs.block.scrollHeight;
            },0)
        }
    }    
}
</script>

<style scoped>
    .c-wrap{
        height: 100%;
        position: relative;
        overflow: hidden;
    }

    .c-form{
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
        padding: 1rem;
        height: 80px;
        background: #212121;
    }

    .c-chat{
        position: absolute;
        bottom: 80px;
        left: 0;
        right: 0;
        top: 0;
        padding: 1rem;
        overflow-y: auto;
    }
</style>