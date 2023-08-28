<template>
  <div class="task-card__check-list">
    <h4 class="task-card__title">
      Чек-лист

      <button
          v-if="!disabled"
          type="button"
          class="task-card__plus"
          @click="$emit('createTick')"
      />

      <!--Кнопка создания новой подзадачи-->
    </h4>
    <!--Список подзадач-->
    <ul
        v-if="ticks.length"
        class="task-card__list"
    >
      <li
          v-for="tick in ticks"
          :key="tick.id || tick.uuid"
          class="task-card__item"
      >
        <div class="task-card__checkbox">
          <label class="checkbox">
            <div class="checkbox__icon">
              <input
                  type="checkbox"
                  name="remember"
                  :checked="tick.done"
                  @click="updateTick(tick, 'done', !tick.done)"
              />
              <span/>
            </div>
            <div class="checkbox__label">
              <input
                  v-if="!disabled"
                  type="text"
                  name="checkbox_name"
                  :value="tick.text"
                  max="64"
                  placeholder="Введите текст пункта"
                  @change="updateTick(tick, 'text', $event.target.value)"
              />
              <span v-else>{{ tick.text }}</span>
            </div>
          </label>
        </div>

        <div
            class="task-card__icons"
            :class="{'task-card__icons--hidden': disabled}"
        >
          <app-icon
              class="icon--trash"
              @click="$emit('removeTick', { uuid: tick.uuid, id: tick.id })"
          />
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import AppIcon from '@/common/components/AppIcon.vue'

const props = defineProps({
  ticks: {
    type: Array,
    default: () => []
  },
  disabled: {
    type: Boolean,
    default: false
  }
})

const emits = defineEmits(['createTick', 'updateTick', 'removeTick'])

const updateTick = function (tick, property, value) {
  const tickCopy = Object.assign({}, tick)
  tickCopy[property] = value
  emits('updateTick', tickCopy)
}
</script>

<style scoped>

</style>
