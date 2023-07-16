<template>
  <div class="container-fluid">
    <h5>Definition</h5>

    <form>
      <div class="mb-3">
        <label class="form-label">Name</label>
        <input
          type="text"
          class="form-control"
          v-model="smartApp.name"
          disabled
        />
      </div>
      <div class="mb-3">
        <label class="form-label">Namespace</label>
        <input
          type="text"
          class="form-control"
          v-model="smartApp.namespace"
          disabled
        />
      </div>
    </form>

    <div class="col-12">
      <h5>Settings</h5>
      Add setting definitions in the source code and then set the values here
    </div>

    <br />
    <h5 class="card-title">OAuth</h5>

    <div v-if="!smartApp.oAuthEnabled">
      <br />
      <button
        class="btn btn-primary"
        outlined
        @click="smartApp.oAuthEnabled = true"
        mx-2
      >
        Enable OAuth in Smart App
      </button>
    </div>
    <div v-else>
      <div class="mb-3">
        <label class="form-label">Client ID</label>
        <input
          type="text"
          class="form-control"
          v-model="smartApp.oAuthClientId"
          placeholder="Public client ID for accessing this SmartApp via its REST API"
          readonly
        />
      </div>
      <div class="mb-3">
        <label class="form-label">Client Secret</label>
        <input
          type="text"
          class="form-control"
          v-model="smartApp.oAuthClientSecret"
          placeholder="Confidential secret key for accessing this SmartApp via its REST API"
          readonly
        />
      </div>
    </div>
    <br />
    <button class="btn btn-primary" @click="updateSmartApp">Update</button>
  </div>
</template>
<script>
export default {
  name: "SmartAppSettings",
  data() {
    return {
      aaId: "",
      smartApp: { oAuthEnabled: false },
    };
  },
  methods: {
    updateSmartApp: function () {
      var body = this.smartApp;
      fetch(`/api/smart-apps/${this.aaId}`, {
        method: "PUT",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(body),
      })
        .then((response) => response.json())
        .then((data) => {
          if (data.success) {
            console.log("success");
          } else {
            console.log("problem saving smart app");
          }
        });
    },
  },

  mounted: function () {
    this.aaId = this.$route.params.id;

    fetch(`/api/smart-apps/${this.aaId}`)
      .then((response) => response.json())
      .then((data) => {
        if (typeof data !== "undefined" && data != null) {
          this.smartApp = data;
        }
      });
  },
};
</script>
<style scoped></style>
