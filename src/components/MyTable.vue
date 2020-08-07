<template>
  <div>
    <button type="button" @click="showModal = true">Добавить</button>
    <table>
      <thead>
      <tr>
        <th>Имя</th>
        <th>Телефон</th>
      </tr>
      </thead>
      <tbody>
      <tr
        v-for="record in records"
        :key="record.id">
        <td>{{ record.name }}</td>
        <td>{{ record.numberPhone }}</td>
      </tr>
      </tbody>
    </table>
    <transition v-if="showModal" name ="modal">
      <form>
        <p>Привет</p>
        <input type="text" ref = "name"/>
        <input type="text" ref = "numberPhone"/>
        <button type="button" @click.prevent="addRow()">Сохранить</button>
      </form>
    </transition>
  </div>
</template>

<script>
export default {
    data: () => ({
        name: '',
        numberPhone: '',
        id: 0,
        records: [
            /*{id: 1, name: 'Vlad', numberPhone: '123'},
            {id: 2, name: 'ivan', numberPhone: '456'},*/
        ],
        showModal: false,
    }),
    methods: {
        addRow () {
            this.name = this.$refs.name.value;
            this.numberPhone = this.$refs.numberPhone.value;
            this.id = this.id++;
            this.records.push({id: this.id, name: this.name, numberPhone: this.numberPhone});
            this.showModal = false;
        }
    }
};
</script>

<style scoped>
h1 {
  font-size: 30px;
}

</style>
