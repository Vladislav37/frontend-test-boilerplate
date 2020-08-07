<template>
  <div>
    <button type="button" @click="showModal = true">Добавить</button>
    <table>
      <thead>
      <tr>
        <th v-for="col in columns" v-bind:key="col">{{ col }}</th>
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
        <input type="text" ref = "name"/>
        <input type="text" ref = "numberPhone"/>
        <select ref="employer">
          <option
                  v-for="rec of records"
                  :key="rec.id"
                  :value="rec.id"
          >{{rec.name}}</option>
        </select>
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
        employer: '',
        records: [],
        columns: [ 'Имя', 'Телефон' ],
        showModal: false,
    }),
    methods: {
        addRow () {
            this.name = this.$refs.name.value;
            this.numberPhone = this.$refs.numberPhone.value;
            this.id = this.id++;
            this.records.push({ id: this.id, name: this.name, numberPhone: this.numberPhone, employer:this.employer });
            this.showModal = false;
            this.name = '';
        }
    }
};
</script>

<style scoped>
h1 {
  font-size: 30px;
}

</style>
