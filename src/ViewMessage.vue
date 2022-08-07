<template>
    <!-- <h1>ViewMessage</h1> -->
    <div class="inbox-body" style="border: 1px solid;">

        <div class="main-option">
            <button class="btn" @click="navigateBack" title="Back">
                <i class="fa fa-arrow-left" aria-hidden="true"></i>&nbsp;
            </button>
            <!-- <strong>|</strong> -->
            <template v-if="typeof data.message.isRead !== 'undefined'" >
                <button v-if="data.message.isRead === true" class="btn" @click="data.message.isRead = false" :disabled="!data.message.isRead" title="Mark as unread">
                    <i class="fa fa-envelope-open" aria-hidden="true"></i>&nbsp;                
                </button>

                <button v-else class="btn" @click="data.message.isRead = true" :disabled="data.message.isRead" title="Mark as read">
                    <i class="fa fa-envelope" aria-hidden="true"></i>&nbsp;                
                </button>
            </template>
            <!-- <strong>|</strong> -->
            <button class="btn" @click="data.message.isDeleted = true" :disabled="data.message.isDeleted">
                <i class="fa fa-trash"></i>&nbsp; {{ data.message.isDeleted ? 'Deleted' : 'Delete'}}
            </button>

        </div>

        <p>
            <h3>{{ data.message.subject }} </h3> 
        </p>
        <p>
            <strong>{{ data.message.from.name }}</strong> &lt; {{ data.message.from.email}} &gt;
        </p>
        <p>
            <strong>{{ data.message.date.fromNow() }} </strong> 
        </p>
        
        <hr>
        <div v-html="data.message.content" class="message"></div>
        <div v-if="data.message.attachments.length > 0" class="attachments">
            <h4>Attachments</h4>
            <ul>
                <li v-for="(attachment, index) in data.message.attachments">
                    <i class="fa fa-paperclip"></i> {{ attachment.fileName }} ({{ attachment.size | formatBytes }})
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    import { eventBus } from './main';

    export default{
        props: {
            data: {
                type: Object,
                required: true
            }
        },
        activated() {
            if(typeof this.data.message.isRead !== 'undefined'){
                this.data.message.isRead = true;
            }
        },
        filters:{
            formatBytes(bytes){
                if(bytes == 0){
                    return '0 Bytes';
                }
                let decimals = 2; 
                let k = 1000;
                let dm = decimals + 1 || 3;
                let sizes = ['Bytes', 'KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB']; 
                let i= Math.floor(Math.log(bytes) / Math.log(k));

                return parseFloat((bytes / Math.pow(k, i)).toFixed (dm)) +' ' + sizes[i];
            }
        },
        methods: {
            navigateBack() {
                let previousView = this.$parent.previousView;
                eventBus.$emit('changeView',{
                    tag: previousView.tag,
                    title: previousView.title,
                    data: previousView.data
                })
            }
        },
    }
</script>