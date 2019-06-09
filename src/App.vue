<template>
  <v-app>
    <v-snackbar
      v-model="snackbarShow"
      bottom
      right
      :timeout="4000"
    >
      Added {{patientName}} as a patient
    </v-snackbar>
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
          <div v-if="error" class="error">An error occured</div>
          <div v-else-if="data" @click="showDialog" class="result">
            Welcome, {{ data.patient.name.first }}
            <Dialog
              @closeModal="showDialog"
              :name="data.patient.name.first"
              :dialog="dialog" />
          </div>
        </template>
      </ApolloQuery>
    </v-toolbar>

    <v-content>
      <PatientTable/>
    </v-content>
    
  </v-app>
</template>

<script>
import patientAddedSubscription from './graphql/Subscriptions/PatientAdded.gql'
import PatientTable from './components/PatientTable'
import Dialog from './components/Dialog'

export default {
  name: 'App',
  components: {
    Dialog,
    PatientTable,
  },
  data() {
    return {
      id: '',
      dialog: false,
      snackbarShow: false,
      patientName: null,
      patient: {
        name: {
          first: 'no data',
        },
      },
    }
  },
  apollo: {
    $subscribe: {
      patientAdded: {
        query: patientAddedSubscription,
        result({ data: { patientAdded } }) {
          this.patientName = patientAdded.name.first
          this.snackbarShow = true
        },
      },
    },
  },
  methods: {
    showDialog() {
      this.dialog = !this.dialog
    },
  },
}
</script>

<style lang="scss">
.v-content {
  &__wrap {
    padding: 2rem;
  }
}
.result {
  cursor: pointer;
  font-weight: 400;
  font-size: 1.3rem;
  color: rgb(66, 66, 66);
}
</style>

