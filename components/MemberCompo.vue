<template>
  <div>
    <a class="member" @click="selectMember(name)">{{ name }}s</a>
  </div>
</template>
<script>
export default {
  props: {
    name: ""
  },
  data() {
    return {};
  },
  methods: {
    selectMember(e) {
      console.log(e);
    }
  }
};
</script>
<style>
.member {
  cursor: pointer;
  font-weight: 900;
}

.selectedMember {
  background-color: lightgreen;
}

.selectedConstraint {
  background-color: red;
}
</style>
