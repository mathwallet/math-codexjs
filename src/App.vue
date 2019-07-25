<template>
  <div id="app">
    <h3>Account -> {{ loginResult }}</h3>
    <button @click="login">log in</button>
    <br />
    <button @click="logout">log out</button>

    <br />
    <br />
    <h3>Transfer -> {{ transferResult }}</h3>
    <button @click="transfer">transfer(codextest->condextest1)</button>
  </div>
</template>
<script>
import Codex from "cdxjs";
export default {
  name: "app",
  data() {
    return {
      nodeCofing: {
        blockchain: "codex",
        httpEndpoint: "https://codex.medishares.net",
        chainId:
          "af776d123b111a53bd6f2333a553e85b99f8ede582ccf28438353cd975f30b83"
      },
      loginResult: "",
      transferResult: "",
      account: null
    };
  },
  methods: {
    login() {
      if (!window.mathExtension) {
        this.loginResult = "Please install mathwallet frist";
        return;
      }
      window.mathExtension.getIdentity(this.nodeCofing).then(a => {
        this.loginResult = `${a.accounts[0].name}@${a.accounts[0].authority}`;
        this.account = a.accounts[0];
      });
    },
    logout() {
      window.mathExtension.forgetIdentity().then(() => {
        this.loginResult = "";
      });
    },
    transfer() {
      if (!this.account) {
        this.transferResult = "Login first";
        return;
      }
      let signProvider = window.mathExtension.codexSignProvider();
      let config = {
        signProvider,
        ...this.nodeCofing
      };
      Codex(config)
        .contract("codex.token")
        .then(token => {
          token
            .transfer(
              this.account.name,
              "codextest1",
              "0.0001 CDX",
              "math extension"
            )
            .then(res => {
              this.transferResult = res.transaction_id;
            })
            .catch(e => {
              this.transferResult = JSON.stringify(e);
            });
        })
        .catch(e => {
          this.transferResult = JSON.stringify(e);
        });
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
