<template>
    <div class="inbox-body">
        <app-messages :messages="sentMessages"></app-messages>
    </div>
</template>

<script>
    import Messages from './Message.vue';
    export default{
        props: {
            data: {
                type: Object,
                required: true
            }
        },
        computed: {
            sentMessages(){
                return this.data.messages.filter(function(message){
                    return (message.type == 'outgoing' && !message.isDeleted);
                });
            },
        },
        components: {
            appMessages: Messages
        }
    }
</script>