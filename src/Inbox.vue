<template>
    <!-- <h1>Inbox</h1> -->
    <div class="inbox-body">
        <div class="mail-option">
            <div class="btn-group">
                <input type="checkbox" />
                <span class="material-icons"> arrow_drop_down </span>
                <!-- <button><span class="material-icons"> refresh </span><button> -->
            
                <a href="#" class="btn" @click.prevent="refresh">
                    <i class="fa fa-refresh"></i>&nbsp; Refresh
                </a>
                <span class="material-icons"> more_vert </span>
            </div>
            
            <div class="emailList__sections" style="padding-top: 1%;">
                <div class="section section__selected">
                    <span class="material-icons"> inbox </span>
                    <h4>Primary</h4>
                </div>

                <div class="section">
                    <span class="material-icons"> people </span>
                    <h4>Social</h4>
                </div>

                <div class="section">
                    <span class="material-icons"> local_offer </span>
                    <h4>Promotions</h4>
                </div>
            </div>
        </div>
        
        <app-messages :messages="incomingMessages"></app-messages>
    </div>
</template>

<script>
    // import Messages from './data/messages';
    import { eventBus } from './main';
    import Messages from './Message.vue';

    export default{
        props: {
            data: {
                type: Object,
                required: true
            }
        },

        methods: {
            refresh(){
                eventBus.$emit('refreshMessages');
            }
        },
        computed: {
            incomingMessages() {
                return this.data.messages.filter(function(message){
                    return (message.type == 'incoming' && !message.isDeleted);
                });
            }
        },

        components: {
            appMessages: Messages
        }
    }
</script>