<template>
  <div>
    <button type="button" @click="showModal = true">Добавить</button>
    <table>
      <thead>
      <tr>
        <th v-for="col in columns"
            v-bind:key="col.idx"
            @click="sortBy(col.desc)">
          {{ col.name }}
        </th>
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
        columns: [
            {idx:0, name:'Имя', desc:'name'},
            {idx:1, name:'Телефон', desc:'numberPhone'}
        ],
        showModal: false,
    }),
    methods: {
        addRow () {
            this.name = this.$refs.name.value;
            this.numberPhone = this.$refs.numberPhone.value;
            this.id = this.records.length;
            this.records.push({ id: this.id, name: this.name, numberPhone: this.numberPhone, employer:this.employer });
            this.showModal = false;
            this.name = '';
            console.log(this.records);
        },
        sortBy (key) {
            this.records.sort((a,b) => {
                console.log(a);
                console.log(b);
                console.log(key);
                return a[key] > b[key] ? -1 : 1;
            })
            console.log(this.records);
        }
    }
};
</script>

<style scoped>
h1 {
  font-size: 30px;
}

th {
  background-color: #42b983;
  color: rgba(255, 255, 255, 0.66);
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

</style>
