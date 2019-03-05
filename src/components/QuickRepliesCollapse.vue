<template>
  <div class="quick-replies-collapse">
    <div class="quick-replies-collapse__description">
      Add quick replies to give your user a set of up to 11 buttons in-conversation.
    </div>
    <div class="quick-replies-collapse__replies">
      <draggable
        v-model="replies"
        handle=".reply__drag-icon"
        @end="onEndDrag"
      >
        <div
          v-for="(reply, idx) in replies"
          :key="reply.id"
          class="reply"
        >
          <div class="reply__drag-icon">
            <img
              :src="DragIcon"
              alt="drag-icon__image"
            >
          </div>
          <ReplyCard
            :title="reply.title"
            :message="reply.payload"
            :looped="reply.is_loop"
            class="reply__card"
            @change-title="(title) => onChangeTitle(idx, title)"
            @change-message="(message) => onChangeMessage(idx, message)"
            @change-looped="(isLoop) => onChangeLooped(idx, isLoop)"
            @delete="onDelete(idx)"
          />
        </div>
      </draggable>
    </div>
    <div class="quick-replies-collapse__adding-btn">
      <img
        :src="AddIcon"
        alt="add-icon"
      >
      <b-button
        variant="link"
        class="add-btn"
        @click="onAdd"
      >
        Add a new text
      </b-button>
    </div>
  </div>
</template>

<script>
import Draggable from 'vuedraggable'
import ReplyCard from '@/components/ReplyCard.vue'
import DragIcon from '@/assets/icons/drag.svg'
import AddIcon from '@/assets/icons/add.svg'

export default {
  name: 'RepliesCollapse',
  components: { Draggable, ReplyCard },
  data() {
    return {
      replies: [
        {
          id: 0, // reply must contain id for reactivity in Vue
          button_type: 'postback',
          order_index: 0,
          title: '☝️ Actualiser',
          payload: 'I will send first',
          is_loop: false,
        },
        {
          id: 1,
          button_type: 'postback',
          order_index: 1,
          title: '☝️ Information Bus',
          payload: 'I will send two',
          is_loop: true,
        },
        {
          id: 2,
          button_type: 'postback',
          order_index: 2,
          title: 'Mes alertes',
          payload: 'I will send 3',
          is_loop: false,
        },
        {
          id: 3,
          button_type: 'postback',
          order_index: 3,
          title: 'Mes alertesR',
          payload: 'I will send 3',
          is_loop: false,
        },
      ],
      drag: false,
      DragIcon,
      AddIcon,
    }
  },
  mounted() {
    this.$emit('change-child-count', this.replies.length) // initial emit to init counters
  },
  methods: {
    recalculateRepliesOrderIdxs() {
      const replies = this.replies.map((reply, idx) => ({
        ...reply,
        order_index: idx,
      }))
      this.replies = [...replies]
    },
    onEndDrag() {
      this.recalculateRepliesOrderIdxs()
    },
    onChangeTitle(idx, title) {
      this.$set(this.replies[idx], 'title', title)
    },
    onChangeMessage(idx, message) {
      this.$set(this.replies[idx], 'payload', message)
    },
    onDelete(idx) {
      this.replies.splice(idx, 1)

      this.$emit('change-child-count', this.replies.length)
    },
    onAdd() {
      const newReplyOrderIdx = this.replies.length
      const newReplyId = this.replies[this.replies.length - 1].id + 1

      this.replies.push({
        id: newReplyId,
        button_type: 'postback',
        order_index: newReplyOrderIdx,
        title: `New Reply${newReplyOrderIdx}`,
        payload: 'I will send new message',
        is_loop: false,
      })

      this.$emit('change-child-count', this.replies.length)
    },
    onChangeLooped(idx, isLoop) {
      this.$set(this.replies[idx], 'is_loop', isLoop)
    },
  },
}
</script>

<style lang="scss" scoped>
.quick-replies-collapse {
  &__description {
    margin-bottom: 20px;
  }

  &__replies {
    margin-bottom: 20px;
  }
}

.reply {
  position: relative;

  &:hover .reply__drag-icon {
    opacity: 1;
  }

  &__drag-icon {
    opacity: 0;
    position: absolute;
    width: 20px;
    left: -20px;
    top: 50%;
    transform: translateY(-50%);
    transition: opacity 0.2s ease-in-out;

    &:hover {
      cursor: pointer;
    }
  }

  &__card {
    margin-bottom: 10px;
  }
}

.add-btn {
  padding: 0;
  font-size: 14px;
}
</style>
