<template>
  <form @submit.prevent="filter">
    <div class="mb-8 mt-4 flex flex-wrap gap-2">

      <div class="flex flex-nowrap items-center gap-1">
        <input v-model.number="filterForm.priceFrom" class="input-form" type="text" placeholder="Price from">
        <input v-model.number="filterForm.priceTo" class="input-form" type="text" placeholder="Price to">
      </div>

      <div class="flex flex-nowrap items-center">
        <select v-model="filterForm.beds">
          <option value="null">Beds</option>
          <option v-for="n in 5" :key="n" :value="n">{{ n }}</option>
          <option>6+</option>
        </select>
        <select v-model="filterForm.baths">
          <option value="null">Baths</option>
          <option v-for="n in 5" :key="n" :value="n">{{ n }}</option>
          <option>6+</option>
        </select>
      </div>

      <div class="flex flex-nowrap items-center gap-1">
        <input v-model.number="filterForm.areaFrom" class="input-form" type="text" placeholder="Area from">
        <input v-model.number="filterForm.areaTo" class="input-form" type="text" placeholder="Area to">
      </div>

      <button class="button-primary" type="submit">Filter</button>
      <button class="button-primary" @click="clear" type="reset">Clear</button>
    </div>
  </form>
</template>

<script setup>

  import {useForm} from '@inertiajs/inertia-vue3'

  const props = defineProps({filters: Object})

  const filterForm = useForm({
    priceFrom: null,
    priceTo: null,
    beds: null,
    baths: null,
    areaFrom: null,
    areaTo: null
  })

  const filter = () => {
    filterForm.get(
      route('listing.index'),
      {
        preserveState: true,
        preserveScroll: true
      }
    )
  }

  const clear = () => {
    filterForm.priceFrom = null
    filterForm.priceTo = null
    filterForm.beds = null
    filterForm.baths = null
    filterForm.areaFrom = null
    filterForm.areaTo = null
  }
</script>