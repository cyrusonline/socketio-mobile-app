<template>
<f7-page name="home">
    <!-- Top Navbar -->
    <f7-navbar :sliding="false" large>
        <f7-nav-left>
            <f7-link icon-ios="f7:menu" icon-aurora="f7:menu" icon-md="material:menu" panel-open="left"></f7-link>
        </f7-nav-left>
        <f7-nav-title sliding>My App {{name}}</f7-nav-title>
        <f7-nav-right>
            <f7-link icon-ios="f7:menu" icon-aurora="f7:menu" icon-md="material:menu" panel-open="right"></f7-link>
        </f7-nav-right>
        <f7-nav-title-large sliding>My App {{name}}</f7-nav-title-large>
    </f7-navbar>

    <!-- Page content-->
    connected : {{connected}}
    <f7-list no-hairlines-md>
        <f7-list-input label="Name" type="text" placeholder="Your name" clear-button :value="name" @input="name = $event.target.value"> </f7-list-input>
        <f7-button fill @click="send">send</f7-button>
        <f7-button fill @click="submit">submit</f7-button>
        <p></p>
        <f7-button fill @click="clear">clear messages</f7-button>

    </f7-list>
    <f7-list>
        <f7-list-item  v-for="message in messages" link="/about/" :title="message"></f7-list-item>
        
    </f7-list>
   

</f7-page>
</template>

<script>
import {
    socket
} from '../js/variables.js'
export default {

    data() {
        return {
            name: null,
            messages: ['adsfsaf','asdfsaf'],
            connected:'nothing to connect'
        }
    },

    methods: {
        vmalert(){
            alert('vm alert')
        },
      clear(){
        this.messages = []
      },
        send() {
            const socket = io('http://10.107.147.190:9000');

            socket.emit('newMessageToServer', {
                text: this.name
            })
        },
        submit(){
            this.messages.push(this.name)
            conn.send(this.name);
        }
    },
    mounted() {
        // const socket = io('http://10.107.147.190:9000');
    

// window.conn.onopen = function(e) {
//     console.log('connected to websocket')
//     //console.log("Connection established!");
// 	this.connected = 'connected to websocket'
// };


    },
    created() {
        const vm = this


        window.conn = new WebSocket('ws://10.107.147.190:8080');

window.conn.onopen = function(e) {
    const self = this
    // console.log('connected to websocket')
    //console.log("Connection established!");
    callvfunction()
};

function callvfunction(){
    console.log('call v function')
  vm.connected = "connect to websocket"
}

window.conn.onmessage = function(e) {
    const self = this
    console.log('message from websocket ',e.data);
    
   appendMessages(e.data)
	
};

function appendMessages(msg){
    const self = this
    console.log('appendmssage')
//     alert('adsfas')
//    alert(vm.connect。ed)
    vm.messages.push(msg)
    // alert(vm.messages)
}
    
           // console.log('socket')
        // console.log(socket)
        // const socket = io('http://10.107.147.190:9000');

        // // socket.on('messageFromServer', (dataFromServer) => {
        // //     alert(dataFromServer)
        // //     // socket.emit('messageToServer',{data:'Data from the client'})
        // // })
        // socket.on('connect', () => {

        //     console.log(socket.id)
        // })

        // socket.on('messageToClients', (msg) => {
        //         this.messages.push(msg.text)

        //     })
        }
}
</script>
