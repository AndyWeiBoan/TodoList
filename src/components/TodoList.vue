<template>
  <div class="align-middle">
    <!-- <h1>{{ msg }}</h1>
    <h1>{{ counter }}</h1>
    <button @click="increment">count</button> -->
    <div class="text-center text-danger my-2">
      <b-container>
        <b-form inline >
          <!-- <label class="sr-only" for="inline-form-input-name">Name</label> -->
            <b-input
              id="inline-form-input-name"
              class="mb-2 mr-sm-2 mb-sm-0"
              placeholder="Jane Doe"
              v-model="alias">{{alias}}
            </b-input>
            <!-- <label class="sr-only" for="inline-form-input-username">Username</label> -->
            <b-input-group prepend="@" class="mb-2 mr-sm-2 mb-sm-0">
              <b-input
              id="inline-form-input-username"
              placeholder="gmail.com"
              v-model="domain"> {{domain}}</b-input>

              <b-input
              id="inline-form-input-username"
              class="mb-2 mr-sm-2 mb-sm-0"
              placeholder="*************"
              v-model="password"> {{password}}</b-input>
            </b-input-group>
          <b-button variant="primary" class="mb-2 mr-sm-2 mb-sm-0" @click="save">Add</b-button>
          <b-button variant="primary" class="mb-2 mr-sm-2 mb-sm-0" @click="clear">Clear</b-button>
          <b-button @click="toggleBusy">Toggle Busy State</b-button>
        </b-form>
        <!-- @row-clicked="dclick" -->
      <b-table responsive striped hover :items="items" :fields="fields" :busy="isBusy">
        <template v-slot:table-busy >
          <div class="text-center text-danger my-2">
            <b-spinner class="align-middle"></b-spinner>
            <strong>Loading...</strong>
          </div>
        </template>

        <template v-slot:cell(actions)="row">
           <b-button size="sm" class="mr-1" @click="edit(row.item.Id)">Edit</b-button>
           <b-button size="sm" class="mr-1">Delete</b-button>
        </template>

        <!-- <template v-slot:cell(Alias)="row">
          <b-form-input v-model="row.item.Alias" v-if="items[row.item.Id === 0 ? 0 : row.item.Id - 1].IsEdit"></b-form-input>
        </template> -->
        <template v-slot:cell(Domain)="row">
          <b-form-input v-model="row.item.Domain" v-if="items[row.item.Id - 1].IsEdit">{{Domain}}</b-form-input>
        </template>
      </b-table>

      <!-- <table class="table table-sm table-dark">
        <thead>
          <tr>
            <th scope="col" v-for="field in fields" :key='field'>{{field.label}}</th>
          </tr>
        </thead>
      </table> -->

      </b-container>
    </div>
  </div>
</template>

<script lang="ts">

import { Component, Prop, Vue } from 'vue-property-decorator'

interface Email {
    Id: number;
    Alias: string;
    Domain: string;
    Password: string;
    IsEdit: boolean;
}
@Component
export default class TodoList extends Vue {
  @Prop() private msg!: string;
  counter = 1;
  items: Email[] = [];
  fields = [
    { key: 'Id', label: 'Id' },
    { key: 'Alias', label: 'Alias' },
    { key: 'Domain', label: 'Domain' },
    { key: 'Password', label: 'Password' },
    { key: 'actions', label: '' },
    { key: 'IsEdit', label: '' }
  ];

  alias = '';
  domain = '';
  password = '';
  Id = 1;
  isBusy = false;
  editable = false;
  increment () {
    this.counter++
  }

  save () {
    this.items.forEach(function (c) { c.IsEdit = false })
    if (this.Id === 6) {
      return
    }
    if (this.alias === '') {
      return
    }
    this.items.push({ Id: this.Id++, Alias: this.alias, Domain: this.domain, Password: this.password, IsEdit: false })
  }

  clear () {
    this.Id = 1
    this.items = []
  }

  toggleBusy () {
    this.isBusy = !this.isBusy
  }

  deletes (index: Email) {
    console.log(index.Id)
  }

  edit (Id: number) {
    console.log(Id)
    this.items[Id - 1].IsEdit = true
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
