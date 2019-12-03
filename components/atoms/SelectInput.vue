<template>
  <div class="select is-rounded">
    <select @change="selectChart">
      <template v-for="(menu, i) in menus">
        <option
          :value="menu.value"
          :key="i"
          :selected="menu.value === selected"
        >
          {{ menu.name }}
        </option>
      </template>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    selected: {
      type: String,
      default: 'PieChart'
    },
    menus: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  methods: {
    selectChart(e) {
      this.$emit('select', e.target.value)
    }
  }
}
</script>
