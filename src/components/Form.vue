<template>
  <v-card>
    <v-card-text>
      <v-form>
        <v-text-field
          v-model="$props.params.title"
          label="제목"
          hide-details />

        <v-btn
          depressed
          color="primary"
          class="mt-4"
          @click="addLists">
          리스트 추가
        </v-btn>

        <div
          v-for="(list, index) in lists"
          :key="index">
          <v-text-field
            v-model="lists[index]"
            label="리스트명"
            hide-details
            @change="changeValue(index)" />
        </div>
      </v-form>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: 'FormComponent',
  props: {
    params: Object
  },
  data() {
    return {
      lists: []
    }
  },
  mounted() {
    this.addLists();
  },
  methods: {
    addLists() {
      this.lists.push('');
      this.$props.params.lists = this.lists;
    },
    changeValue(index) {
      this.$props.params.lists[index] = this.lists[index];
    }
  }
}
</script>