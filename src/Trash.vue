<template>
    <!-- <h1>Trash</h1> -->
    <div class="inbox-body">
        <app-messages :messages="trashMessages"></app-messages>
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
            trashMessages(){
                return this.data.messages.filter(function(message){
                    return message.isDeleted === true;
                });
            },
        },
        components: {
            appMessages: Messages
        }
    }
</script>