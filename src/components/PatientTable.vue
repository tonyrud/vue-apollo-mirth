<template>
    <div class="patient-table">
        <h1 class="patient-table__heading">Patients</h1>
        <v-data-table
            :headers="headers"
            :items="patients"
            :pagination.sync="pagination"
            class="elevation-1"
        >
      <template v-slot:items="props">
        <td>{{ props.item.name && props.item.name.first }}</td>
        <td>{{ props.item.name && props.item.name.last }}</td>
        <td >{{ props.item.phone && props.item.phone.home }}</td>
        <td >{{ props.item.birthDate }}</td>
        <td >{{ props.item.lastUpdated }}</td>
        <td >{{ props.item.gender }}</td>
        <td >{{ props.item.practitioner.name.full }}</td>
      </template>
      <template v-slot:pageText="props">
        Lignes {{ props.pageStart }} - {{ props.pageStop }} de {{ props.itemsLength }}
      </template>
    </v-data-table>
    </div>
</template>

<script>
import PatientsQuery from "../graphql/Queries/Patients.gql";
export default {
  name: "PatientTable",
  apollo: {
    patients: PatientsQuery
  },
  data() {
    return {
      pagination: {
        rowsPerPage: 10
      },
      headers: [
        {
          text: "First",
          align: "left",
          sortable: false,
          value: "first"
        },
        {
          text: "Last",
          align: "left",
          sortable: false,
          value: "last"
        },
        { text: "Phone", value: "phone", sortable: false },
        { text: "Birth Date", value: "bd", sortable: false },
        { text: "Last Updated", value: "last-updated", sortable: false },
        { text: "Gender", value: "gender", sortable: false },
        { text: "Practitioner", value: "practitioner", sortable: false }
      ]
    };
  }
};
</script>

<style scoped rel="stylesheet/scss" lang="scss" type="text/scss">
.patient-table {
  &__heading {
    margin-bottom: 0.8rem;
  }
}
</style>