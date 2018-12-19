<template>
  <div class="item" :class="{checked : task.checked}">
    <div class="check" @click="check">
      <span class="icon">
        <font-awesome-icon icon="check" />
      </span>
    </div>
    <div>
      <p>{{task.text}}</p>
      <small>{{humanize(task.date)}}</small>
    </div>
    <a @click="$emit('delete')" class="btn delete">
      <font-awesome-icon icon="trash" />
    </a>
  </div>
</template>
<script>
import moment from 'moment';
export default {
  name: 'list-item',
  props: ['task'],
  methods: {
    check () {
      this.task.checked = !this.task.checked
      this.$emit('check')
    },
    humanize: (date) => moment(date).locale('es').fromNow()
  }
}
</script>
<style scoped>
.item {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 4fr 1fr;
  align-items: center;
  padding: 12px 0;
  border-bottom: 1px solid gray;
  border-radius: 8px;
}
.item.checked p {
  text-decoration: line-through;
}
.check {
  border: 1px solid var(--primary-text);
  display: flex;
  width: 35px;
  height: 35px;
  color: #fff;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  align-self: center;
  justify-self: center;
  transition: .3s;
  cursor: pointer;
}
.check .icon {
  transition: .5s;
  opacity: 0;
}
.item.checked .check .icon {
  opacity: 1;
}
.item.checked .check {
  border: 0;
  background: var(--green-one);
} 
.delete {
  justify-self: center;
  padding: 10px;
  background: var(--error);
}
.delete:hover {
  background: var(--error-ligth);
}
p {
  font-size: 17px;
  font-weight: 600;
}
</style>
