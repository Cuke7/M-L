<template>
    <div id="app">
        <Tinder key-name="id" :queue.sync="queue" :offset-y="10" @submit="onSubmit">
            <template slot-scope="scope">
                <div class="pic" :style="{ backgroundImage: `url(${scope.data.id}` + ')' }" />
            </template>
            <img class="like-pointer" slot="like" src="./assets/like-txt.png" />
            <img class="nope-pointer" slot="nope" src="./assets/nope-txt.png" />
            <img class="super-pointer" slot="super" src="./assets/super-txt.png" />
        </Tinder>
    </div>
</template>

<script>
import Tinder from "vue-tinder";
import source from "@/bing2";

export default {
    name: "App",
    components: { Tinder },
    data: () => ({
        queue: [],
        offset: 0,
        liked: [],
    }),
    created() {},
    methods: {
        mock(count = source.length - 1) {
            const list = [];
            for (let i = 0; i < count; i++) {
                list.push({ id: source[this.offset] });
                this.offset++;
            }
            this.queue = this.queue.concat(list);
        },
        onSubmit(type, key, item) {
            // if (this.queue.length < 3) {
            //     this.mock();
            // }
            console.log(type, item);
            if (type.type == "like") {
                let toto = type.key;
                this.liked.push(toto);
            }
            console.log(this.liked);
        },
    },
    mounted() {
        // let images = require.context("@/assets/images/", true);
        // this.source = images.keys();
        // console.log(images.keys());
        this.mock();
    },
};
</script>

<style>
html,
body {
    height: 100%;
}

body {
    margin: 0;
    background-color: #20262e;
    overflow: hidden;
}

#app .vue-tinder {
    position: absolute;
    z-index: 1;
    left: 0;
    right: 0;
    top: 23px;
    bottom: 46px;
    margin: auto;
    min-width: 300px;
    max-width: 355px;
}

.nope-pointer,
.like-pointer {
    position: absolute;
    z-index: 1;
    top: 20px;
    width: 64px;
    height: 64px;
}

.nope-pointer {
    right: 10px;
}

.like-pointer {
    left: 10px;
}

.super-pointer {
    position: absolute;
    z-index: 1;
    bottom: 80px;
    left: 0;
    right: 0;
    margin: auto;
    width: 112px;
    height: 78px;
}

.pic {
    width: 100%;
    height: 100%;
    background-size: cover;
    background-position: center;
}
</style>
