<script setup lang="ts">
import { ref, onMounted } from 'vue';
import axios from 'axios';

interface Deal{
  name: String,
  status: String,
  ResponsiblePerson: String,
  date: String,
  Budget: Number
}

const Deals = ref<Array<Deal>>([
  { name: "--------", status: "-----------------", ResponsiblePerson: "-------------", date: "-----" , Budget: 0 },
  { name: "--------", status: "-----------------", ResponsiblePerson: "-------------", date: "-----" , Budget: 0 },
  { name: "--------", status: "-----------------", ResponsiblePerson: "-------------", date: "-----" , Budget: 0 }
])

let textField: string

const getData = async () => {
  if(textField.length >= 3){
    try {
      let res = await axios.get("http://localhost:8014/api/getData", {params: {filterName : textField}})
      Deals.value = res.data
    } catch(err){
      console.log(err);
    }
  }
}

onMounted(async () => {
  try {
    let res = await axios.get("http://localhost:8014/api/getData")
    Deals.value = res.data
  } catch(err){
    console.log(err);
  }
})
</script>

<template>
<div class="d-flex justify-space-around pt-16">
  <span class="text-h4">Сделки компании "Тестоваое задание"</span>
  <div class="d-flex">
    <v-responsive
      width="344"
    >
      <v-text-field
        label="Название сделки"
        single-line
        hide-details
        v-model="textField"
      ></v-text-field>
    </v-responsive>
    <v-btn icon="mdi-magnify" variant="text" class="mx-2" @click="getData"></v-btn>
  </div>
</div>

<v-table height="60vh" fixed-header class="pa-8">
    <thead>
      <tr>
        <th class="text-left">
          Название
        </th>
        <th class="text-left">
          Статус
        </th>
        <th class="text-left">
          Ответсвенное лицо
        </th>
        <th class="text-left">
          Дата создания
        </th>
        <th class="text-left">
          Бюджет
        </th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="deal in Deals"
      >
        <td>{{ deal.name }}</td>
        <td>{{ deal.status }}</td>
        <td>{{ deal.ResponsiblePerson }}</td>
        <td>{{ deal.date }}</td>
        <td>{{ deal.Budget }}₽</td>
      </tr>
    </tbody>
  </v-table>
</template>
