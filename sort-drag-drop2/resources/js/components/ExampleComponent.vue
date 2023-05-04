<template>
    <div class="container" ref="dragAreaRef">
        <div class="item" v-for="(item, index) in items" :key="index" :data-id="item.id">
            <div class="image">
                <img :src='item.image'/>
            </div>
            <div class="name">
                <span>{{ item.name }}</span><br>
                <p>{{ item.author }}</p>
            </div>
            <div class="drag-icon"><i class="fa fa-bars" aria-hidden="true"></i></div>
        </div>
    </div>
</template>

<script>
import Sortable from 'sortablejs';
import axios from 'axios';

export default {
    props: {
        initData: {
            default: []
        }
    },
    data() {
        return {
            items: [],
            order: []
        };
    },
    created: function () {
        this.initData.forEach(item => {
            this.items.push(item)
        });
    },
    mounted() {

        const dragArea = this.$refs.dragAreaRef;
        new Sortable(dragArea, {
            animation: 350,
            onEnd: function (evt) {
                const newOrder = this.toArray();
                this.order = newOrder;
                axios.post('api/update-order', { newOrder: newOrder })
                    .then(response => {
                        console.log(response.data);
                    })
                    .catch(error => {
                        console.log(error);
                    });
            },
        });
    }
};
</script>
<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
}

body {
    display: flex;
    background: #fff;
    padding: 10px;
}
</style>
<style scoped>
.container {
    background: #fff;
    padding: 5px;
    max-width: 460px;
    width: 100%;
    border-radius: 10px;
    border: 1px solid #ccc

}
.container .item {
    cursor: pointer;
    display: flex;
    margin-bottom: 2px;
    padding: 5px;
}
.item:hover{
    background: #dfece7;
    transition: 0.4;
    border-radius: 10px;
}
.image{
    width: 100px;height: 60px;
}
.image > img{
    width: 100%;height: 100%;border-radius: 10px;
}
.name{
    width: calc(100% - 120px);padding: 5px;font-size: 90%;padding-bottom: 0;
}
.name > p{
    font-size: 95%;opacity: 0.5;margin-top: 4px;
}
.drag-icon{
    width: 20px;line-height: 55px;
}
</style>
