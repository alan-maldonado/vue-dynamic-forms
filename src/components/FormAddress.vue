<template>
  <div>
    <h1 class="title">Delivery details</h1>

    <h2 class="subtitle">
      Where should we send your freshly roasted coffee beans?
    </h2>

    <form @input="submit" class="form">
      <div class="form-group">
        <label class="form-label" for="delivery_name">Name</label>
        <input v-model="$v.form.recipient.$model" type="text" placeholder="Recipients Name" class="form-control"
          id="delivery_name">
        <div v-if="$v.form.recipient.$error" class="error">field is required</div>
      </div>

      <div class="form-group">
        <label class="form-label" for="address">Address</label>
        <textarea v-model="$v.form.address.$model" placeholder="London Street 470978 New England" rows="3"
          class="form-control" id="address"></textarea>
        <div v-if="$v.form.address.$error" class="error">field is required</div>
      </div>
    </form>
  </div>
</template>

<script>
import { required } from 'vuelidate/lib/validators'
export default {
  props: {
    wizardData: {
      type: Object,
      required: true,
    }
  },
  data() {
    return {
      form: {
        address: this.wizardData.address,
        recipient: this.wizardData.name,
      }
    }
  },
  // watch: {
  //   'wizardData.name' (value) {
  //     this.form.recipient = value
  //   }
  // },
  activated () {
    this.form.recipient = this.wizardData.name
  },
  validations: {
    form: {
      address: {
        required
      },
      recipient: {
        required
      }
    }
  },
  methods: {
    submit() {
      this.$emit('update', {
        data: {
          recipient: this.form.recipient,
          address: this.form.address,
        },
        valid: !this.$v.$invalid,
      })
    }
  }
}
</script>

<style scoped></style>