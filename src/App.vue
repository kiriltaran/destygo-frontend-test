<template>
  <div id="app">
    <div class="wrapper">
      <div class="wrapper__inner">
        <ACollapse>
          <ACollapseItem
            v-for="(item, idx) in collapseItems"
            :id="String(idx)"
            :key="idx"
            :expanded="activeCollapseIdx === idx"
            @expand="onExpand(idx)"
            @hide="onHide(idx)"
          >
            <template v-slot:header>
              <img
                :src="item.icon"
                alt="collapse-icon"
                class="collapse-item-header__icon"
              >
              <span class="collapse-item-header__title">{{ item.title }}</span>
              <b-badge
                pill
                :variant="item.childCount ? 'primary' : 'secondary'"
              >
                {{ item.childCount }}
              </b-badge>
            </template>
            <component
              :is="item.content"
              @change-child-count="(count) => onChangeChildCount(idx, count)"
            />
          </ACollapseItem>
        </ACollapse>
      </div>
    </div>
  </div>
</template>

<script>
import { ACollapse, ACollapseItem } from '@/components/shared/ACollapse'
import TextContentCollapse from '@/components/TextContentCollapse.vue'
import QuickRepliesCollapse from '@/components/QuickRepliesCollapse.vue'

import FlashIcon from '@/assets/icons/flash.svg'
import TextReplyIcon from '@/assets/icons/text-reply.svg'

export default {
  name: 'App',
  components: {
    ACollapse,
    ACollapseItem,
    TextContentCollapse,
    QuickRepliesCollapse,
  },
  data() {
    return {
      collapseItems: [
        {
          title: 'Text content',
          content: TextContentCollapse,
          icon: TextReplyIcon,
          childCount: 0,
        },
        {
          title: 'Templates',
          content: TextContentCollapse,
          icon: FlashIcon, // duplicate flash icon cause of invalid img icon(assets/img.svg)
          childCount: 0,
        },
        {
          title: 'Quick replies',
          content: QuickRepliesCollapse,
          icon: FlashIcon,
          childCount: 0,
        },
      ],
      activeCollapseIdx: null,
    }
  },
  methods: {
    onExpand(idx) {
      this.activeCollapseIdx = idx
    },
    onHide(idx) {
      if (this.activeCollapseIdx === idx) {
        this.activeCollapseIdx = null
      }
    },
    onChangeChildCount(idx, count) {
      this.$set(this.collapseItems[idx], 'childCount', count)
    },
  },
}
</script>

<style lang="scss">
html,
body,
#app {
  height: 100%;
  color: #555;
}

.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;

  &__inner {
    width: 800px;
  }
}

.collapse-item-header {
  &__icon {
    margin-right: 15px;
  }
  &__title {
    margin-right: 10px;
  }
}
</style>
