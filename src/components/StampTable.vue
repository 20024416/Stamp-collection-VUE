<template>
  <table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Value (€)</th>
        <th>Color</th>
        <th>Image</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="stamp in stamps" :key="stamp.id">
        <td>{{ stamp.name }}</td>
        <td>{{ stamp.value }}</td>
        <td>{{ stamp.color }}</td>
        <td><img :src="`${stamp.image}`" alt="Stamp Image"></td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'StampTable',
  props: {
    stamps: {
      type: Array,
      required: true
    }
  }
};
</script>
