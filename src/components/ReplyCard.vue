<template>
  <b-card class="reply-card">
    <div
      :class="['reply-card__header', {'reply-card__header--expanded': expanded}]"
    >
      <input
        v-if="expanded"
        :value="title"
        type="text"
        class="header-input"
        @input="onInputTitle"
      >
      <span
        v-else
        class="header-title"
      >
        {{ title }}
      </span>
      <div class="actions">
        <div
          class="actions__expand"
          @click="onToggleExpand"
        >
          <span class="expand-icon">{{ expanded ? '▲' : '▼' }}</span>
        </div>
        <div
          class="actions__delete"
          @click="onClickDelete"
        >
          <img
            :src="BinIcon"
            alt="delete__image"
          >
        </div>
      </div>
    </div>
    <div :class="['reply-card__body', {'reply-card__body--expanded': expanded}]">
      <div class="message-subtitle">
        Message sent to bot
      </div>
      <input
        :value="message"
        type="text"
        class="message-input"
        @input="onInputMessage"
      >
      <span class="loop-subtitle">This quick reply has to loop</span>
      <ToggleButton
        :value="looped"
        :width="40"
        :height="20"
        class="loop-switcher"
        @input="onToggleLooped"
      />
    </div>
  </b-card>
</template>

<script>
import { ToggleButton } from 'vue-js-toggle-button'
import BinIcon from '@/assets/icons/bin.svg'

export default {
  name: 'ReplyCard',
  components: {
    ToggleButton,
  },
  props: {
    title: {
      type: String,
      required: true,
    },
    message: {
      type: String,
      required: true,
    },
    looped: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      expanded: false,
      BinIcon,
    }
  },
  methods: {
    onClickDelete() {
      this.$emit('delete')
    },
    onInputTitle(e) {
      this.$emit('change-title', e.target.value)
    },
    onInputMessage(e) {
      this.$emit('change-message', e.target.value)
    },
    onToggleLooped(isLooped) {
      this.$emit('change-looped', isLooped)
    },
    onToggleExpand() {
      this.expanded = !this.expanded
    },
  },
}
</script>

<style lang="scss" scoped>
.reply-card {
  &__header {
    display: flex;
    justify-content: space-between;
    align-items: center;

    &--expanded {
      margin-bottom: 20px;
    }
  }

  &__body {
    height: 0;
    overflow: hidden;

    &--expanded {
      height: auto;
    }
  }
}

.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;

  &:hover {
    cursor: pointer;
  }
}

.expand-icon {
  font-size: 16px;
  margin-right: 10px;
}

.header-title {
  font-weight: 600;
}

.header-input {
  width: 150px;
  border: none;
  border-bottom: 1px dashed #555;
  font-weight: 600;
  color: #555;
}

.message-subtitle {
  font-size: 12px;
  margin-bottom: 5px;
}

.message-input {
  width: 100%;
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 8px;
  margin-bottom: 20px;
}

.loop-subtitle {
  margin-right: 10px;
}
</style>
