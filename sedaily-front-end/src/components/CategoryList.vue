<template>
<div class='categories'>
  <span class='category-post' @click="setSelectedCategory({name: 'All', id: null})" :class='getClassForCategory("All")'>All</span>
  <span v-for="category in categories"
    :key="category.id"
    @click="setSelectedCategory(category)"
    class='category-post'
    :class='getClassForCategory(category.name)'>{{category.name}}</span>
</div>
</template>

<script>

export default {
  name: 'category-list',
  props: {
    categories: {
      type: Array,
      required: true
    },
    activeCategory: {
      type: Object,
      required: false
    }
  },
  methods: {
    setSelectedCategory (category) {
      this.$emit('setSelectedCategory', category)
    },
    getClassForCategory (categoryName) {
      return (this.activeCategory && this.activeCategory.name === categoryName) ? 'category-active' : ''
    }
  }
}
</script>

<style lang="stylus" scoped>
@import './../css/variables'

.categories
  margin-bottom 10px
  display flex
  flex-direction column
  align-items flex-start 
  @media (max-width 600px)
    overflow auto
    white-space nowrap

.category-post
  text-align center
  display inline-block
  cursor pointer
  color grey
  padding 5px 10px
  border-radius 25px
  &:hover
    color white
    background primary-color

.category-active
  border 1px solid primary-color
  color white
  background primary-color
  &:hover
    border-radius 25px
</style>
