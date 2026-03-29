<script setup>
defineProps({
  columns: {
    type: Array,
    required: true
    // Each: { key: string, label: string, align?: 'left' | 'center' | 'right', width?: string }
  },
  rows: {
    type: Array,
    required: true
    // Each row is an object with keys matching column.key
    // Each cell can be: string | { text: string, color?: string, bgColor?: string, bold?: boolean }
  },
  variant: { type: String, default: 'default' }, // 'default' | 'financial' | 'heatmap' | 'harvey'
  caption: { type: String, default: '' }
})
</script>

<template>
  <div class="data-table" :class="[`variant-${variant}`]">
    <table>
      <thead>
        <tr>
          <th
            v-for="col in columns"
            :key="col.key"
            :style="{ textAlign: col.align || 'left', width: col.width }"
          >
            <span v-html="col.label"></span>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, rIdx) in rows" :key="rIdx" :class="row._rowClass">
          <td
            v-for="col in columns"
            :key="col.key"
            :style="getCellStyle(row[col.key], col)"
          >
            <span v-if="typeof row[col.key] === 'object'" :style="getCellTextStyle(row[col.key])">
              {{ row[col.key].text }}
            </span>
            <span v-else>{{ row[col.key] }}</span>
          </td>
        </tr>
      </tbody>
    </table>
    <div v-if="caption" class="caption">{{ caption }}</div>
  </div>
</template>

<script>
export default {
  methods: {
    getCellStyle(cell, col) {
      const base = { textAlign: col.align || 'left' }
      if (typeof cell === 'object' && cell.bgColor) {
        base.backgroundColor = cell.bgColor
      }
      return base
    },
    getCellTextStyle(cell) {
      const style = {}
      if (cell.color) style.color = cell.color
      if (cell.bold) style.fontWeight = 600
      return style
    }
  }
}
</script>

<style scoped>
.data-table {
  margin: 1rem auto;
  max-width: 700px;
}

table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.75rem;
}

thead tr {
  border-bottom: 2px solid #111;
}

th {
  padding: 0.5rem 0.6rem;
  font-weight: 600;
}

tbody tr {
  border-bottom: 1px solid #e5e7eb;
}

tbody tr:last-child {
  border-bottom: none;
}

td {
  padding: 0.5rem 0.6rem;
}

/* Financial variant */
.variant-financial th:first-child,
.variant-financial td:first-child {
  font-weight: 500;
}

.variant-financial td:not(:first-child) {
  text-align: right;
}

/* Heatmap variant */
.variant-heatmap td {
  text-align: center;
  font-weight: 600;
}

/* Harvey balls variant */
.variant-harvey td {
  text-align: center;
  font-size: 1.3rem;
}

.caption {
  margin-top: 0.5rem;
  font-size: 0.7rem;
  color: #888;
  text-align: center;
}
</style>
