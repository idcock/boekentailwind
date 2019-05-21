Skip to content Why GitHub? Enterprise Explore Marketplace Pricing Search Sign
in Sign up 0 0 0 StevenCVO/boekentailwind Code Issues 0 Pull requests 0 Projects
0 Insights Join GitHub today GitHub is home to over 36 million developers
working together to host and review code, manage projects, and build software
together. boekentailwind/src/components/DataTabel.vue unknown Update 288166b 7
days ago 146 lines (138 sloc) 3.8 KB

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

          <i @click="sorteren(kolom.veld)" class="material-icons cursor-pointer"
            >arrow_upward</i
          >
        </th>
      </tr>
    </thead>
    <tbody>
      <tr class="border" v-for="item of gepagineerd" :key="item[itemKey]">
        <td class="p-2" v-for="kolom of kolommen" :key="kolom.veld">
          {{ getWaardeViaVeld(item, kolom.veld) }}
        </td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <td :colspan="kolommen.length">
          <div class="flex justify-end py-4 px-10 items-center">
            <div class="mx-4">Rijen per pagina</div>
            <select class="mx-4 border-b" v-model="perPagina">
              <option value="5">5</option>
              <option value="10">10</option>
              <option value="15">15</option>
              <option :value="items.length">Alles</option>
            </select>
            <div class="mx-4">
              {{ (huidigePagina - 1) * perPagina + 1 }} -
              {{ Math.min(huidigePagina * perPagina, items.length) }}
              van {{ items.length }}
            </div>
            <i
              @click="navigeerPagina(-1)"
              :class="{ 'opacity-25': huidigePagina === 1 }"
              class="material-icons cursor-pointer"
              >keyboard_arrow_left</i
            >
            <i
              @click="navigeerPagina(1)"
              :class="{ 'opacity-25': huidigePagina === aantalPaginas }"
              class="material-icons cursor-pointer"
              >keyboard_arrow_right</i
            >
          </div>
        </td>
      </tr>
    </tfoot>
  </table>
</template>

<script>
export default {
  data() {
    return {
      perPagina: 5,
      huidigePagina: 1,
      sorteerveld: "",
      richting: "asc"
    };
  },
  props: {
    titel: {
      type: String,
      default: "Titel"
    },
    items: {
      type: Array,
      // zelfde als:
      // function() {
      //   return []
      // }
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
  },
  computed: {
    aantalPaginas() {
      return Math.ceil(this.items.length / this.perPagina);
    },
    gesorteerd() {
      if (!this.sorteerveld) {
        return this.items;
      }
      return this.items.slice().sort((a, b) => {
        const waarde1 = this.getWaardeViaVeld(a, this.sorteerveld).toString();
        const waarde2 = this.getWaardeViaVeld(b, this.sorteerveld).toString();
        return waarde1.localeCompare(waarde2, undefined, { numeric: true });
      });
    },
    gepagineerd() {
      return this.gesorteerd.slice(
        (this.huidigePagina - 1) * this.perPagina,
        Math.min(this.huidigePagina * this.perPagina, this.items.length)
      );
    }
  },
  methods: {
    getWaardeViaVeld(obj, veldString) {
      // obj is bv. boek
      // veldString is bv. "auteur.naam"
      // String omzetten naar array van velden
      const veldArray = veldString.split(".");
      // Zoeken in de diepte vanuit het startobject
      return veldArray.reduce((res, veld) => {
        return res[veld];
      }, obj);
    },
    navigeerPagina(aantal) {
      this.huidigePagina = Math.max(1, this.huidigePagina + aantal);
      this.huidigePagina = Math.min(this.aantalPaginas, this.huidigePagina);
    },
    sorteren(veld) {
      this.sorteerveld = veld;
    }
  }
};
</script>

<style></style>
