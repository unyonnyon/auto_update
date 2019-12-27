<template>
    <v-app>
        <v-content app>
            <v-container fluid>
                <v-row justify="center" class="mb-4">
                    <v-timeline>
                        <v-timeline-item>innerWidth: {{width}}</v-timeline-item>
                        <v-timeline-item class="text-right">timeline item</v-timeline-item>
                        <v-timeline-item>innerHeight: {{height}}</v-timeline-item>
                    </v-timeline>
                </v-row>
                <v-row justify="center">
                    <v-btn rounded dark @click="openDialog">
                        <v-icon>cached</v-icon>
                    </v-btn>
                </v-row>
            </v-container>
        </v-content>
    </v-app>
</template>

<script>

const { dialog } = require('electron').remote

export default {

    name: "App",
    data: () => ({
        width: window.innerWidth,
        height: window.innerHeight,
        getPaths: []
    }),
    methods: {
        handleResize() {
            this.width = window.innerWidth;
            this.height = window.innerHeight;
        },
        openDialog(){
            dialog.showOpenDialog({ properties: ['openFile', 'multiSelections'] })
            .then(result => {
                console.log(result);
                this.getPaths = result.filePaths;
            })
        }
    },
    mounted() {
        window.addEventListener("resize", this.handleResize);
    },
    beforeDestroy: function() {
        window.removeEventListener("resize", this.handleResize);
    }
};
</script>
