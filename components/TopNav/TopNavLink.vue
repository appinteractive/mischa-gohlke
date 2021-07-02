<template>
  <router-link
  v-if="to"
    v-slot="{ href, navigate }"
    class="flex cursor-pointer"
    tag="div"
    :to="to"
  >
    <a
      role="link"
      :href="href"
      :class="[
        isActive
          ? 'text-gray-900'
          : 'text-gray-500 hover:text-primary-700',
      ]"
      @click="navigate"
    >
      <slot />
    </a>
  </router-link>
  <div v-else class="inline cursor-pointer" role="link">
    <slot />
  </div>
</template>

<script>
export default {
  props: {
    to: { type: [String, Object], default: null }
  },
  computed: {
    isActive() {
      const pathItems = this.$route.fullPath.split('/')
      const current = pathItems.pop()
      const path = pathItems.join('/')
      const root = this.to.split('/')[1]

      if (path && this.to.includes(path)) {
        return true
      }
      if (path.includes(root)) {
        return true
      }
      if (current && this.to.includes(current)) {
        return true
      }
      return false
    }
  },
}
</script>
