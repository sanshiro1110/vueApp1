<template>
  <div>
    <div class="container">
      <div class="date">
        <h3>日付</h3>
        <p>
          <span class="changeButton" @click="prevDay">&lt;</span>
          {{ inputData.year }}年{{ inputData.month }}月{{ inputData.date }}日
          <span class="changeButton" @click="nextDay">&gt;</span>
        </p>
      </div>

      <div class="category">
        <h3>カテゴリー</h3>
        <select v-model="inputData.category">
          <option v-for="category in categories" :key="category">{{ category }}</option>
        </select>
      </div>

      <div class="payment">
        <h3>支出額</h3>
        <input type="number" min="0" id="payment" v-model="inputData.payment">
        <span>円</span>
      </div>

      <div class="memo">
        <h3>メモ</h3>
        <textarea name="diary" id="" cols="30" rows="5" v-model="inputData.diary"></textarea>
      </div>
    </div>
    <div class="buttonArea">
      <button class="save" @click="dataRequest">記録する</button>
    </div>
  </div>
</template>

<style scoped>
  .container > div {
    padding: 4.5%;
  }

  .container > div:not(:last-child) {
    border-bottom: 1px solid #000;
  }

  .container > div h3 {
    margin-bottom: 12px;
  }

  .changeButton {
    cursor: pointer;
    display: inline-block;
    border: 1px solid #2c3e50;
    padding: 2px;
    user-select: none;
  }

  .buttonArea {
    margin-top: 20px;
  }

  .save {
    cursor: pointer;
  }

  .category select {
    padding: 3px;
  }
</style>

<script>
import * as firebase from 'firebase';

const today = new Date();

export default {
  data() {
    return {
      inputData: {
        year: today.getFullYear(),
        month: today.getMonth() + 1,
        date: today.getDate(),
        category: "食費",
        payment: 0,
        diary: "",
        id: 0,
      },
      categories: ["食費", "日用品", "美容品", "交際費", "交通費", "その他"],
    }
  },
  computed: {
    getUsersDocumentId() {
      return this.$store.getters.idToken;
    }
  },
  methods: {
    prevDay() {
      this.inputData.date --;
      if(this.inputData.month == 3 || this.inputData.month == 5 || this.inputData.month == 7 || this.inputData.month == 10 || this.inputData.month == 12) {
        if(this.inputData.date < 1) {
          this.inputData.month --;
          this.inputData.date = 30;
        }
      } else {
        if(this.inputData.date < 1) {
          this.inputData.month --;
          this.inputData.date = 31;
        }
      }
      if(this.inputData.month < 1) {
        this.inputData.month = 12;
        this.inputData.year --;
      }
    },
    nextDay() {
      this.inputData.date ++;
      if(this.inputData.month == 2 || this.inputData.month == 4 || this.inputData.month == 6 || this.inputData.month == 9 || this.inputData.month == 11) {
        if(this.inputData.date > 30) {
          this.inputData.month ++;
          this.inputData.date = 1;
        }
      } else {
        if(this.inputData.date > 31) {
          this.inputData.month ++;
          this.inputData.date = 1;
        }
      }
      if(this.inputData.month > 12) {
        this.inputData.month = 1;
        this.inputData.year ++;
      }
    },
    dataRequest() {
      if(this.inputData.payment == 0) {
        alert('※支出額が0円です');
      }
      if(this.inputData.payment !== 0) {
        alert('保存されました');
        const db = firebase.firestore();
        db.collection('users').doc(this.getUsersDocumentId).collection('postData').add({
          year: this.inputData.year,
          month: this.inputData.month,
          date: this.inputData.date,
          category: this.inputData.category,
          payment: parseInt(this.inputData.payment),
          diary: this.inputData.diary,
        }).then(response => {
          db.collection('users')
          .doc(this.getUsersDocumentId)
          .collection('postData')
          .doc(response.id).set({
            id: response.id
          }, { merge: true });
          this.inputData.category = "食費";
          this.inputData.payment = 0;
          this.inputData.diary = "";
        });
      }
    },
  },
}
</script>

