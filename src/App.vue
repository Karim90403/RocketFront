<script setup lang="ts">
import { ref } from 'vue';


interface Deal{
  name: String,
  status: String,
  ResponsiblePerson: String,
  date: String,
  Budget: Number
}

const Deals = ref<Array<Deal>>([
  { name: "Сделка 1", status: "Первичный контакт", ResponsiblePerson: "Первичный контакт", date: "20 января 2023" , Budget: 1000 },
  { name: "Сделка 2", status: "Первичный контакт", ResponsiblePerson: "Первичный контакт", date: "20 января 2023" , Budget: 1000 },
  { name: "Сделка 3", status: "Первичный контакт", ResponsiblePerson: "Первичный контакт", date: "20 января 2023" , Budget: 1000 },
  { name: "Сделка 4", status: "Первичный контакт", ResponsiblePerson: "Первичный контакт", date: "20 января 2023" , Budget: 1000 },
])
</script>

<template>
<div class="d-flex justify-space-around pt-16">
  <span class="text-h4">Сделки компании "Тестоваое задание"</span>
  <v-responsive
    max-width="344"
  >
  <v-text-field
    append-icon="mdi-magnify"
    label="Search"
    single-line
    hide-details
  ></v-text-field>
  </v-responsive>
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
        <th class="text-left"></th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="deal in Deals"
        :key="deal.name"
      >
        <td>{{ deal.name }}</td>
        <td>{{ deal.status }}</td>
        <td>{{ deal.ResponsiblePerson }}</td>
        <td>{{ deal.date }}</td>
        <td>{{ deal.Budget }}₽</td>
        <td><v-btn density="compact" icon="mdi-plus"></v-btn></td>
      </tr>
    </tbody>
  </v-table>
</template>
