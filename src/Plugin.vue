<template>
  <div>
    <label class="uk-margin-right uk-margin-bottom uk-display-inline-block" v-for="tag in tags">
      <input type="checkbox" v-bind:value="tag.name" v-model="model.tags" class="uk-margin-small-right">
      {{ tag.name }}
    </label>
  </div>
</template>

<script>
export default {
  mixins: [window.Storyblok.plugin],
  data() {
    return {
      tags: []
    }
  },
  methods: {
    initWith: function() {
      return {
        plugin: 'taglist',
        tags: []
      }
    }
  },
  events: {
    'plugin:created': function() {
      this.api(`spaces/${this.spaceId}/tags`).get().then((res) => {
        this.tags = res.data.tags
      })
    }
  },
  watch: {
    'model': {
      handler: function (value) {
        this.$emit('changed-model', value);
      },
      deep: true
    }
  }
}
</script>

<style>

</style>
