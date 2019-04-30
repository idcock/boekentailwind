<template>
  <table class="w-full">
    <caption class="bg-blue-500 text-white text-xl p-4">
      <div class="flex flex-row justify-between items-center">
        <span class="font-semibold">{{ titel }}</span>
        <slot name="titel-knop"></slot>
      </div>
    </caption>
    <thead>
      <tr>
        <th
          class="text-left p-2 border-b"
          v-for="kolom of kolommen"
          :key="kolom.veld"
        >
          {{ kolom.naam }}
        </th>
      </tr>
    </thead>
    <tbody>
      <tr class="border" v-for="item of items" :key="item[itemKey]">
        <td class="p2" v-for="kolom of kolommen" :key="kolom.veld">
          {{ item[kolom.veld] }}
        </td>
      </tr>
    </tbody>
    <tfoot></tfoot>
  </table>
</template>

<script>
export default {
  props: {
    titel: {
      type: String,
      default: "titel"
    },
    items: {
      type: Array,
      // idem als
      // default: function(){
      // return [] }
      default: () => []
    },
    itemKey: {
      type: String,
      default: "_id"
    },
    kolommen: {
      type: Array,
      default: () => []
    }
  }
};
</script>

<style></style>
