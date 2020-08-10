<template>
  <div>
    <button
        type="button"
        @click="showModalWindow"
    >
        Добавить
    </button>
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

    <ModalWindow
            v-if="visibleModalWindow"
            titleButton = "Сохранить"
            modalWindowTitle = "Дополнительная информация"
            @closeModalWindow = "closeModalWindow"
            @addRecordFromModalWindow = "addNewRecordToGrid"
    >
        <form>
            <div></div>
            <div>
                <label>Имя</label>
                <input type="text" ref="name"/>
            </div>
            <div>
                <label>Телефон</label>
                <input type="text" ref="numberPhone"/>
            </div>
            <div>
                <label>Начальник</label>
                <!--<select ref="employer">-->
                    <!--<option-->
                            <!--v-for="rec of records"-->
                            <!--:key="rec.id"-->
                            <!--:value="rec.id"-->
                    <!--&gt;-->
                        <!--{{rec.name}}-->
                    <!--</option>-->
                <!--</select>-->
                <MySelect
                        :options="records"
                        :selected="selected"
                        @select="selectEmployer"
                />
            </div>
        </form>
    </ModalWindow>

  </div>
</template>

<script>
import ModalWindow from '@/components/ModalWindow'
import MySelect from '@/components/SelectForModalWindow'

export default {
    data: () => ({
        name: null,
        numberPhone: null,
        id: null,
        employer: null,
        records: [],
        columns: [
            {idx:0, name:'Имя', desc:'name'},
            {idx:1, name:'Телефон', desc:'numberPhone'}
        ],
        visibleModalWindow: false,
        orderSortName: 'desc',
        orderSortPhone: 'desc',
        selected: '123',
    }),
    components: {
        ModalWindow,
        MySelect
    },
    beforeMount() {
        window.addEventListener('beforeunload', this.beforeRefresh);
    },
    mounted() {
        this.$nextTick(function () {
            let cacheRecords = JSON.parse(localStorage.getItem('recordsFromTable'));
            if (cacheRecords.length > 0) this.records = cacheRecords;
        });
    },
    methods: {
        selectEmployer (record) {
            this.selected = record.name;
        },
        showModalWindow () {
            this.visibleModalWindow = true;
        },
        closeModalWindow () {
            this.visibleModalWindow = false;
        },
        addNewRecordToGrid () {
            this.name = this.$refs.name.value;
            this.numberPhone = this.$refs.numberPhone.value;
            this.id = this.records.length;
            this.records.push({ id: this.id, name: this.name, numberPhone: this.numberPhone, employer:this.employer });
            this.visibleModalWindow = false;
            this.name = '';
        },
        beforeRefresh () {
            localStorage.setItem('recordsFromTable', JSON.stringify(this.records));
        },
        sortBy (key) {
            if (key === 'name') {
                this.orderSort('orderSortName', key);
            } else if (key === 'numberPhone') {
                this.orderSort('orderSortPhone', key);
            }
        },
        orderSort (prop, key) {
            this.records.sort((a,b) => {
                if (this[prop] === 'desc') {
                    return a[key] > b[key] ? -1 : 1;
                } else {
                    return a[key] < b[key] ? -1 : 1;
                }
            });
            this[prop] = (this[prop] === 'desc' ? 'asc' : 'desc');
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
