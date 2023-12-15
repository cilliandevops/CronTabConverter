<template>
  <div class="cron-converter">
    <div class="header">
      <h1>希里安 Linux-Crontab 转换器</h1>
    </div>
    <div class="converter-box">
      <el-form :model="toRefs(form)">
        <el-form-item label="分钟" class="form-item">
          <el-select v-model="form.minute" placeholder="选择分钟" class="select">
            <el-option label="每分钟" value="*"></el-option>
            <el-option v-for="n in 59" :key="n" :label="n" :value="n.toString()"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="小时" class="form-item">
          <el-select v-model="form.hour" placeholder="选择小时" class="select">
            <el-option label="每小时" value="*"></el-option>
            <el-option v-for="n in 23" :key="n" :label="n" :value="n.toString()"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="日期" class="form-item">
          <el-select v-model="form.day" placeholder="选择日期" class="select">
            <el-option label="每天" value="*"></el-option>
            <el-option v-for="n in 31" :key="n" :label="n" :value="n.toString()"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="月份" class="form-item">
          <el-select v-model="form.month" placeholder="选择月份" class="select">
            <el-option label="每月" value="*"></el-option>
            <el-option v-for="n in 12" :key="n" :label="n" :value="n.toString()"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="星期几" class="form-item">
          <el-select v-model="form.week" placeholder="选择星期几" class="select">
            <el-option label="每天" value="*"></el-option>
            <el-option label="星期日" value="0"></el-option>
            <el-option label="星期一" value="1"></el-option>
            <el-option label="星期二" value="2"></el-option>
            <el-option label="星期三" value="3"></el-option>
            <el-option label="星期四" value="4"></el-option>
            <el-option label="星期五" value="5"></el-option>
            <el-option label="星期六" value="6"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item class="button-container">
          <el-button type="primary" @click="convert" class="convert-button">转换</el-button>
        </el-form-item>
      </el-form>
      <!-- <el-alert v-if="crontab" title="转换结果" type="success" class="result-alert">{{ crontab }}</el-alert> -->
      <el-card v-if="crontab" class="result-card">
    <div slot="header" class="clearfix">
      <!-- <span>结果</span> -->
    </div>
    <div class="terminal">
      {{ crontab }}
    </div>
  </el-card>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, toRefs } from 'vue';

export default defineComponent({
  name: 'CronTabConverter',
  setup() {
    const form = reactive({
      minute: '*',
      hour: '*',
      day: '*',
      month: '*',
      week: '*',
    });

    const crontab = ref('');

    function convert() {
      crontab.value = `${form.minute} ${form.hour} ${form.day} ${form.month} ${form.week}`;
    }

    return {
      form,
      crontab,
      convert,
      toRefs,
    };
  },
});
</script>

<style scoped>
.cron-converter {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-align: center;
  padding: 2rem;
  background: linear-gradient(35deg, #667eea 40%, #764ba2 60%,#52afb1, #9e28a0);
  background-size: 400% 400%;
  color: #1a1b1d;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  animation: AnimationName 10s ease infinite;

}

@keyframes AnimationName { 
  0%{background-position:0% 30%}
  50%{background-position:80% 50%}
  100%{background-position:0% 30%}
}

.header h1 {
  font-size: 2rem;
  margin-bottom: 1.5rem;
}

.converter-box {
  background: rgba(250, 243, 243, 0.959);
  backdrop-filter: blur(10px);
  border-radius: 15px;
  padding: 2rem;
  max-width: 500px;
  width: 100%;
}

.form-item {
  margin-bottom: 1rem;
}

.select {
  width: 100%;
}

.button-container {
  margin-top: 1.5rem;
}

.convert-button {
  width: 100%;
  border: none;
  background: #ff7675;
  color: #ffffff;
  font-size: 1rem;
  padding: 0.75rem 1.5rem;
  letter-spacing: 1px;
  transition: background-color 0.3s;
}

.convert-button:hover {
  background: #b451e2;
}

.result-card {
  margin-top: 30px;
  border: 1px solid #333;
  background-color: #000;
  color: #00ff00;
  padding: 0rem; /* 添加内边距 */
}

.result-card .terminal {
  font-family: 'Courier New', Courier, monospace;
  font-size: 2.25rem;
  white-space: pre; /* 保持格式，例如空格和换行 */
}

.result-card .clearfix {
  color: #fff;
  padding: 0.5rem 1rem; /* 为标题部分添加内边距 */
}

</style>
