<template>
  <div :class="['a-collapse-item', {'a-collapse-item--expanded': expanded} ]">
    <div
      v-b-toggle="id"
      :class="['a-collapse-item__header', {'a-collapse-item__header--expanded': expanded}]"
      role="tab"
    >
      <slot name="header" />
    </div>
    <b-collapse
      :id="id"
      :visible="expanded"
      accordion="accordion"
      role="tabpanel"
      class="a-collapse-item__body"
      @show="onShow"
      @hide="onHide"
    >
      <slot />
    </b-collapse>
  </div>
</template>

<script>
export default {
  name: 'ACollapseItem',
  props: {
    id: {
      type: String,
      required: true,
    },
    expanded: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    onShow() {
      this.$emit('expand')
    },
    onHide() {
      this.$emit('hide')
    },
  },
}
</script>

<style lang="scss" scoped>
.a-collapse-item {
  padding: 15px;
  border: 1px solid #ddd;

  &:first-child {
    border-top-right-radius: 5px;
    border-top-left-radius: 5px;
  }

  &:last-child {
    border-bottom-right-radius: 5px;
    border-bottom-left-radius: 5px;
  }

  &--expanded {
    border-left: 3px solid #009ad6;
  }

  &__header {
    position: relative;
    font-size: 18px;
    font-weight: 500;

    &:hover {
      cursor: pointer;
    }

    &:after {
      content: '►';
      color: #888;
      position: absolute;
      right: 0;
      top: 50%;
      transform: translateY(-50%);
      font-size: 12px;
    }

    &--expanded {
      &:after {
        content: '▼';
      }
    }
  }

  &__body {
    color: #888;
    padding: 0 40px;
    font-size: 14px;
  }
}
</style>
