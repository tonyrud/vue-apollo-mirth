<template>
    <v-dialog
      v-model="dialog"
      width="500"
    >

      <v-card>
        <v-card-title
          class="headline grey lighten-2"
          primary-title
        >
          Edit User
        </v-card-title>

        <v-card-text>
           <v-form ref="form">
                <v-text-field
                v-model="inputName"
                label="Name"
                ></v-text-field>
            </v-form>

        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn @click="submit">submit</v-btn>
          <v-btn
            color="primary"
            flat
            @click="$emit('closeModal')"
          >
            Close
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
</template>

<script>
export default {
  name: "Dialog",
  props: {
    dialog: {
      type: Boolean,
      default: false
    },
    name: {
      type: String
    }
  },
  data() {
    return {
      inputName: this.name
    };
  },
  methods: {
    submit() {
      console.log("form submitted", this.inputName);
    }
  }
};
</script>

<style scoped rel="stylesheet/scss" lang="scss" type="text/scss">
</style>