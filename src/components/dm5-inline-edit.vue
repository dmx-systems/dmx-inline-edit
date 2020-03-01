<template>
  <div :class="['dm5-inline-edit', mode]">
    <slot name="info" v-if="infoMode"></slot>
    <slot name="form" v-else></slot>
    <!-- Edit Button -->
    <el-button class="edit fa fa-pencil" v-if="showEdit" type="text" @click="edit"></el-button>
    <!-- Save Button -->
    <el-button class="save-button" v-if="showSave" @click.stop="save">Save</el-button>
  </div>
</template>

<script>
export default {

  mixins: [
    require('./mixins/info-mode').default
  ],

  data () {
    return {
      mode: 'info'    // 'info' or 'form'
    }
  },

  computed: {

    showEdit () {
      // inline editing can only be started in info mode
      return this.infoMode    // && this.editable
    },

    showSave () {
      return this.formMode
    }
  },

  methods: {

    edit () {
      this.mode = 'form'
    },

    save () {
      this.mode = 'info'
      this.$emit('save')
    }
  }
}  
</script>

<style>
.dm5-inline-edit {
  position: relative;     /* for absolute positioned "edit" button */
}

.dm5-inline-edit.info:hover {
  background-color: white;
}

/* Edit Button */

.dm5-inline-edit button.edit {
  position: absolute;
  bottom: 0;
  right: -12px;
  visibility: hidden;
  padding: 0 !important;
}

.dm5-inline-edit:hover button.edit {
  visibility: visible;
}
</style>
