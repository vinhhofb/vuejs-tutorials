<template>
    <div class="container">
        <div class="title">
            <h3>Tags</h3>
        </div>
        <div class="details">
            <button @click="removeAllTags">Remove All</button>
        </div>
        <div style="clear: both;"></div>
        <div class="content">
            <ul>
                <li v-for="(tag, index) in tags" :key="index">{{ tag }} <i class="fa fa-trash-o"
                        @click="removeTag(index)"></i></li>
                <input type="text" spellcheck="false" v-model.trim="newTag" @keyup.enter="addTag">
            </ul>
        </div>
        <button class="submit" @click="submitTags" :disabled="disabled">Save</button>
    </div>
</template>

<script>
export default {
    props: {
        initTags: {
            default: []
        }
    },
    data() {
        return {
            tags: [],
            newTag: "",
            disabled: false
        };
    },
    created: function () {
        this.initTags.forEach(tag => {
            this.tags.push(tag)
        });
    },
    methods: {
        addTag() {
            const newTags = this.newTag
                .split(",")
                .map((tag) => tag.trim())
                .filter((tag) => tag && !this.tags.includes(tag));
            if (newTags.length > 0 && this.tags.length + newTags.length <= 10) {
                this.tags.push(...newTags);
            }
            this.newTag = "";
        },
        removeTag(index) {
            this.tags.splice(index, 1);
        },
        removeAllTags() {
            this.tags = [];
        },
        submitTags() {
            this.disabled = true;
            axios.post('/api/save-tags', {
                data: JSON.stringify(this.tags)
            })
            .then(response => {
                if(response?.data?.status){
                    this.disabled = false;
                }
            })
            .catch(error => {
                console.log(error);
            });
        }
    },
};
</script>
<style>
/* Import Google Font - Poppins */
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap');

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
}

body {
    display: flex;
    background: #05a645;
    padding: 10px;
}

.container {
    width: 100%;
    background: #fff;
    padding: 12px;
}

.container :where(.title, li, li i, .details) {
    display: flex;
    align-items: center;
}

.title {
    float: left;
}

.details {
    float: right;
}

.content ul {
    display: flex;
    flex-wrap: wrap;
    margin: 12px 0;
    border: 1px solid #a6a6a6;
    padding: 5px;
}

.content ul li {
    margin: 4px 3px;
    list-style: none;
    background: #F2F2F2;
    padding: 5px;
    font-size: 12px;
}

.content ul li i {
    height: 20px;
    width: 20px;
    margin-left: 8px;
    font-size: 12px;
    cursor: pointer;
    background: #fff;
    justify-content: center;
    text-align: center;
    line-height: 20px;
}

.content ul input {
    flex: 1;
    padding: 5px;
    border: none;
    outline: none;
    font-size: 12px;
}

.details {
    justify-content: space-between;
}

.details button {
    border: none;
    outline: none;
    color: #fff;
    font-size: 12px;
    cursor: pointer;
    padding: 5px 15px;
    background: #05a645;
}

.submit {
    border: none;
    outline: none;
    color: #fff;
    font-size: 12px;
    padding: 5px 15px;
    background: #05a645;
    width: 100%;
}
button:disabled{
    opacity: 0.7;
}
</style>
