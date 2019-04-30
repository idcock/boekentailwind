<template>
  <div>
    <img
      class="w-1/4 mx-auto mb-8"
      src="@/assets/images/boeken.jpg"
      alt="afbeelding boeken"
    />
    <table class="w-full">
      <caption class="bg-blue-500 text-white text-xl p-4">
        <div class="flex flex-row justify-between items-center">
          <span class="font-semibold">Boekbeheer</span>
          <button class="border-2 rounded p-2 hover:bg-blue-300">
            Nieuw boek
          </button>
        </div>
      </caption>
    </table>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: "home",
  components: {}
};
</script>
