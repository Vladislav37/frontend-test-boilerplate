<template>
    <div class="body">
        <div class="commonDivForButtonAndGrid">
            <button
                class="addButton"
                type="button"
                @click="showModalWindow"
            >
                Добавить
            </button>
            <div class="gridDiv">
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
            </div>
        </div>

        <ModalWindow
                v-if="visibleModalWindow"
                titleButton = "Сохранить"
                modalWindowTitle = "Добавление пользователя"
                @closeModalWindow = "closeModalWindow"
                @addRecordFromModalWindow = "addNewRecordToGrid"
        >
            <form>
                <div class="divForInput">
                    <label>Имя:</label>
                    <input type="text" ref="name"/>
                </div>
                <div class="divForInput">
                    <label>Телефон:</label>
                    <input type="text" ref="numberPhone"/>
                </div>
                <div class="divForInput">
                    <label>Начальник:</label>
                    <select ref="employer">
                        <option
                                v-for="rec of records"
                                :key="rec.id"
                                :value="rec.id"
                        >
                            {{rec.name}}
                        </option>
                    </select>
                    <!-- Попытка сделать кастомный select :) -->
                    <!--<MySelect-->
                            <!--:options="records"-->
                            <!--:selected="selected"-->
                            <!--@select="selectEmployer"-->
                    <!--/>-->
                </div>
            </form>
        </ModalWindow>
    </div>
</template>

<script>
import ModalWindow from '@/components/ModalWindow'
//import MySelect from '@/components/SelectForModalWindow'

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
        //MySelect
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
        // selectEmployer (record) {
        //     this.selected = record.name;
        //     this.employer = record.name;
        // },
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
.divForInput {
    display: flex;
    padding: 10px 10px;
}

.divForInput label {
    flex: 30%;
}

.divForInput input {
    flex: 50%;
}

.divForInput select {
    flex: 70%;
}

.commonDivForButtonAndGrid {
    width: 50%;
}

.addButton {
    color: #fff;
    background: #42b983;
    border: 0;
    border-radius: 8px;
    padding: 10px 20px;
}

h1 {
  font-size: 30px;
}

table {
    border: 2px solid #42b983;
    border-radius: 3px;
    background-color: #fff;
}

th {
    background-color: #42b983;
    color: #fff;
    cursor: pointer;
    user-select: none;
}

td {
    background-color: #f9f9f9;
}

th,
td {
    min-width: 120px;
    padding: 10px 20px;
}
</style>
