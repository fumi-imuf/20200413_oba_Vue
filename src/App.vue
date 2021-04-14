<template>
  <div id="app">
    <div class="main">
      <div class="main-container">
        <h1 class="head">Todo List</h1>
        <div class="input-container">
          <input type="text" class="new-input" v-model="list">
          <button class="add" @click="insertList">追加</button>
        </div>
        <table class="table">
          <tr class="tr" v-for="item in todoList" :key="item.id">
            <td><input type="text" v-model="item.list"></td>
            <div class="edit-button">
            <td><button class="update" @click="updateList(item.id, item.list)">更新</button></td>
            <td><button class="delete" @click="deleteList(item.id)">削除</button></td>
            </div>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios"
export default {
  data() {
    return {
      list: "",
      todoList: ""
    };
  },
  methods: {
    async getList() {
      const resData = await axios.get("https://pure-meadow-60471.herokuapp.com/api/todolist");
      this.todoList = resData.data.data;
    },
    async insertList() {
      const sendData = { list: this.list };
      await axios.post("https://pure-meadow-60471.herokuapp.com/api/todolist", sendData);
      await this.getList();
      this.list = "";
    },
    async updateList(id, list) {
      const sendData = { list: list };
      await axios.put("https://pure-meadow-60471.herokuapp.com/api/todolist/" + id, sendData);
      await this.getList();
    },
    async deleteList(id) {
      await axios.delete("https://pure-meadow-60471.herokuapp.com/api/todolist/" + id);
      await this.getList();
    }
  },
  created() {
    this.getList();
  }
};
</script>

<style scoped>
/* リセットcss */
html, body, div, span, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
abbr, address, cite, code,
del, dfn, em, img, ins, kbd, q, samp,
small, strong, sub, sup, var,
b, i,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, figcaption, figure,
footer, header, hgroup, menu, nav, section, summary,
time, mark, audio, video {
    margin:0;
    padding:0;
    border:0;
    outline:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}

body {
    line-height:1;
}

article,aside,details,figcaption,figure,
footer,header,hgroup,menu,nav,section {
    display:block;
}

nav ul {
    list-style:none;
}

blockquote, q {
    quotes:none;
}

blockquote:before, blockquote:after,
q:before, q:after {
    content:'';
    content:none;
}

a {
    margin:0;
    padding:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}

/* change colours to suit your needs */
ins {
    background-color:#ff9;
    color:#000;
    text-decoration:none;
}

/* change colours to suit your needs */
mark {
    background-color:#ff9;
    color:#000;
    font-style:italic;
    font-weight:bold;
}

del {
    text-decoration: line-through;
}

abbr[title], dfn[title] {
    border-bottom:1px dotted;
    cursor:help;
}

table {
    border-collapse:collapse;
    border-spacing:0;
}

/* change border colour to suit your needs */
hr {
    display:block;
    height:1px;
    border:0;  
    border-top:1px solid #cccccc;
    margin:1em 0;
    padding:0;
}

input, select {
    vertical-align:middle;
}

html {
  background-color: #15202b;
}
* {
  color: white;
  font-family: "Noto Sans JP";
}
/* リセットcssここまで */

.main {
  background-color: #2D197C;
  height: 100vh;
  width: 100vw;
  position: relative;
}

.main-container {
  background-color: #fff;
  width: 50vw;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 10px;
  padding: 30px;
}

/* h1 todolist */
.head {
  font-size: 24px;
  font-weight: bold;
  color: black;
}

.input-container {
  display: flex;
  justify-content: space-between;
  margin: 10px 0;
}

/* input共通 */
input {
  border: 1px solid #ccc;
  border-radius: 5px;
  color: black;
  padding: 5px;
}

.new-input {
  width: 80%;
}


/* button共通 */
button {
  border-radius: 5px;
  font-size: 12px;
  font-weight: bold;
  background-color: #fff;
  cursor: pointer;
  padding: 5px 10px ;
  transition: 0.5s;
  outline: none;
  margin: 2px;
}

/* add button */
.add {
  border: 2px solid #dc70fa;
  color: #dc70fa;
  font-size: 12px;
  font-weight: bold;
  background-color: #fff;
  cursor: pointer;
}
.add:hover {
  background-color: #dc70fa;
  color: #fff;
}

/* uqdate button */
.update {
  border: 2px solid #fa9770;
  color: #fa9770;
  font-size:12px;

}
.update:hover {
  background-color: #fa9770;
  color: #fff;
}

/* delete button */
.delete {
  border: 2px solid #71fadc;
  color: #71fadc;
}

.delete:hover {
  background-color: #71fadc;
  color: #fff; 
}

.table {
  width: 100%;
}

.tr {
display: flex;
justify-content: space-between;
}

table td input {
  width: 20vw;
}

</style>

