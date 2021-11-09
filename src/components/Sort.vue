<template>
    <table>
        <thead>
            <tr>
                <th @click="sortByColumn('id')">ID
                    <span v-if="sortColumn == 'id'" class="material-icons">{{arrowIconName}}</span>
                    <span v-else class="material-icons">sort</span>
                </th>
                <th @click="sortByColumn('name')">Name
                    <span v-if="sortColumn == 'name'" class="material-icons">{{arrowIconName}}</span>
                    <span v-else class="material-icons">sort</span>
                </th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="row in tableData" :key="row.id">
                <td>{{row.id}}</td>
                <td>{{row.name}}</td>
            </tr>
        </tbody>
    </table>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
    setup() {
        interface dataInfo {
            id: number,
            name: string
        }

        let data: Array<dataInfo> = [
            {"id": 1, "name": "Phil"},
            {"id": 2, "name": "Bobby"},
            {"id": 3, "name": "Susie"},
        ];
        const tableData = ref(data);

        const sortColumn = ref("id");
        const sortDirection = ref(1);
        const arrowIconName = ref("arrow_drop_up");

        const sortByColumn = (columnName: keyof dataInfo) => {
            sortColumn.value = columnName;
            sortDirection.value = -1 * sortDirection.value;

            if (sortDirection.value == 1) {
                arrowIconName.value = "arrow_drop_up";
                tableData.value.sort((a, b) => (a[columnName] > b[columnName] ? 1 : -1));
            } else {
                arrowIconName.value = "arrow_drop_down";
                tableData.value.sort((a, b) => (a[columnName] < b[columnName] ? 1 : -1));
            }
        }

        return {tableData, sortColumn, sortDirection, arrowIconName, sortByColumn};
    },
})
</script>

<style scoped>
table {
    border-collapse: collapse;
    margin: auto;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
}

thead tr {
    background-color: gray;
    color: white;
}

tbody tr {
    border-bottom: 1px solid black;
}

th, td {
    padding: 12px 15px;
}

.material-icons {
    vertical-align: -6px;
}

th {
    cursor: pointer;
}
</style>