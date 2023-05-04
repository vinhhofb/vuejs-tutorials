<template>
  <div class="wrapper" ref="dragAreaRef">
    <div class="item" v-for="(item, index) in items" :key="index" :data-id="item.id">
      <span class="text">{{ item.name }}</span>
      <i class="fas fa-bars"></i>
    </div>
  </div>
</template>

<script>
import Sortable from 'sortablejs';
import axios from 'axios';

export default {
  data() {
    return {
      items: [
        {
          id: '1',
          name: 'Draggable Element One1',
        },{
          id: '2',
          name: 'Draggable Element One2',
        },{
          id: '3',
          name: 'Draggable Element One3',
        },{
          id: '4',
          name: 'Draggable Element One4',
        },{
          id: '5',
          name: 'Draggable Element One5',
        }
      ],
      order: []
    };
  },
  mounted() {
    const dragArea = this.$refs.dragAreaRef;
    new Sortable(dragArea, {
      animation: 350,
      onEnd: function (evt) {
        const newOrder = this.toArray();
        this.order = newOrder;
        axios.post('/updateOrder', { newOrder: newOrder })
      .then(response => {
        // handle the response from the backend
        console.log(response.data);
      })
      .catch(error => {
        // handle the error
        console.log(error);
      });
      },
    });
  },
  methods: {
    save(){
      console.log("d");
    }
  }
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background: #304B5F;
  padding: 20px;
}

.wrapper {
  background: #fff;
  padding: 25px;
  max-width: 460px;
  width: 100%;
  border-radius: 3px;
  box-shadow: 0px 10px 15px rgba(0, 0, 0, 0.1);
}

.wrapper .item {
  color: #fff;
  display: flex;
  margin-bottom: 8px;
  padding: 12px 17px;
  background: #304B5F;
  border-radius: 3px;
  align-items: center;
  justify-content: space-between;
  cursor: pointer;
}

.wrapper .item:last-child {
  margin-bottom: 0px;
}

.wrapper .item .text {
  font-size: 18px;
  font-weight: 400;
}

.wrapper .item i {
  font-size: 18px;
  cursor: pointer;
}</style>