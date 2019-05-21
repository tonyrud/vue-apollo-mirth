<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Graphql</span>
        <span class="font-weight-light">fhir</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <ApolloQuery
        :query="require('./graphql/Queries/Patient.gql')"
        :variables="{ id }"
      >
        <template slot-scope="{ result: { loading, error, data } }">
          <div v-if="loading" class="loading">Loading...</div>
          <div v-else-if="error" class="error">An error occured</div>
          <div v-else-if="data" class="result">Welcome, {{ data.patient.name.full }}</div>
          <div v-else class="no-result apollo">No result :(</div>
        </template>
      </ApolloQuery>

        <!-- <span class="mr-2">Welcome, {{patient.name.first}}</span> -->
    </v-toolbar>

    <v-content>
      <PatientTable/>
    </v-content>
  </v-app>
</template>

<script>
import PatientTable from "./components/PatientTable";
// import PatientQuery from "./graphql/Patient.gql";

export default {
  name: "App",
  components: {
    PatientTable
  },
  // apollo: {
  //   patient: PatientQuery
  // },
  data() {
    return {
      id: "",
      patient: {
        name: {
          first: "no data"
        }
      }
    };
  }
};
</script>

<style lang="scss">
.v-content__wrap {
  padding: 2rem;
}
</style>

