<template>
  <div class="body">
    <section>
      <div class="choice" @dragover.prevent @dragenter="dragEnterHandler" @dragleave="dragLeaveHandler" @drop="dropHandler">
        <div class="title">Todo</div>
        <div class="content" v-for="(item, index) in items" :key="index" @dragstart="dragStartHandler" @dragend="dragEndHandler" draggable="true">
          <p class="task-title">{{ item.title }}</p>
          <p class="date">{{ item.start }} ~ {{ item.end }}</p>
          <p class="member">{{ item.member }}</p>
        </div>
      </div>
      <div class="choice" @dragover.prevent @dragenter="dragEnterHandler" @dragleave="dragLeaveHandler" @drop="dropHandler">
        <div class="title">In Progress</div>
      </div>
      <div class="choice" @dragover.prevent @dragenter="dragEnterHandler" @dragleave="dragLeaveHandler" @drop="dropHandler">
        <div class="title">Complete</div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'DragDrop',
  data() {
    return {
      items: [
        {
          title: 'Lorem Ipsum is simply dummy text simply dummy text.',
          member: 'HHV',
          start: '2023/07/07',
          end: '2023/07/12'
        },{
          title: 'Lorem Ipsum is simply dummy text simply dummy text.',
          member: 'HHV',
          start: '2023/07/07',
          end: '2023/07/12'
        },{
          title: 'Lorem Ipsum is simply dummy text simply dummy text.',
          member: 'HHV',
          start: '2023/07/07',
          end: '2023/07/12'
        },{
          title: 'Lorem Ipsum is simply dummy text simply dummy text.',
          member: 'HHV',
          start: '2023/07/07',
          end: '2023/07/12'
        },{
          title: 'Lorem Ipsum is simply dummy text simply dummy text.',
          member: 'HHV',
          start: '2023/07/07',
          end: '2023/07/12'
        }
      ],
      dragItem: null,
      dropTarget: null
    };
  },
  methods: {
    dragStartHandler(e) {
      this.dragItem = e.target;
    },
    dragEndHandler() {
      this.dragItem = null;
    },
    dragEnterHandler(e) {
      e.target.classList.add('highlight');
      this.dropTarget = e.target;
    },
    dragLeaveHandler(e) {
      e.target.classList.remove('highlight');
      this.dropTarget = null;
    },
    dropHandler() {
      if (this.dropTarget) {
        this.dropTarget.classList.remove('highlight');
        this.dropTarget.appendChild(this.dragItem);
      }
    }
  }
};
</script>


<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap');
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}
  .title{
    width: 100%;
    padding: 4px;
    background: #dde2ea;
    font-weight: bold;
    margin-bottom: 10px;
  }
  .body{
    width: 100%;
    height: 100vh;
    background: #428ff5;
    padding-left: 10px;
    padding-right: 10px;
    padding-top: 10px;
  }
  section {
    width: 100%;
    height: calc(100vh - 10px);
    display: flex;
    justify-content: space-around;
  }
  .choice {
    width: 300px;
    height: 95%;
    padding: 8px;
    margin: 10px;
    background: #dde2ea;
    box-sizing: border-box;
  }
  .choice > .content {
    background: #fff;
    padding: 10px;
    margin-bottom: 10px;
  }
  .highlight{
    border: 5px solid #fff;
  }
  .task-title{
    line-height: 18px;
    font-size: 90%;
    font-weight: 500;
  }
  .date{
    font-size: 80%;
    margin-top: 5px;
  }
  .member{
    margin-top: 10px;
    background: #e8e5fc;
    display: inline-block;
    padding-left: 7px;
    padding-right: 7px;
    border-radius: 5px;
    font-size: 90%;
  }
</style>