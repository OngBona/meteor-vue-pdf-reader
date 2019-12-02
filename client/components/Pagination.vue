<template>
  <div class="pdf-pagination">
    <div class="pre">
      <button :class="{ disabled: currentPage <= 1 }" @click="pre">
        Prev
      </button>
    </div>
    <!-- <input
      class="current-page"
      v-model="currentPage"
      @keypress="isNumber($event)"
    /> -->
    <input v-model.number="currentPage" @change="iChangePage" />
    <div class="next">
      <button :class="{ disabled: currentPage >= total }" @click="next">
        Next
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    total: {
      required: true,
      type: Number,
      default: 1
    }
  },
  data() {
    return {
      currentPage: 1
    };
  },
  watch: {
    currentPage: function(val, oldVal) {
      // if(!!val) return;
      // if (val < 1 || val > this.total) {
      //   this.currentPage = oldVal;
      //   return;
      // }

      this.$emit("pageChange", this.currentPage);
    }
  },
  methods: {
    next() {
      this.currentPage < this.total && this.currentPage++;
    },
    iChangePage() {
      this.currentPage < this.total && this.currentPage;
    },
    pre() {
      this.currentPage > 1 && this.currentPage--;
    },
    isNumber: function(evt) {
      evt = evt ? evt : window.event;
      var charCode = evt.which ? evt.which : evt.keyCode;
      if (charCode > 31 && (charCode < 48 || charCode > 57) && charCode != 9) {
        evt.preventDefault();
      } else {
        return true;
      }
    }
  }
};
</script>
<style scoped>
.pdf-pagination {
  font-size: 0;
  text-align: center;
}
.pre,
.current-page,
.next {
  display: inline-block;
  font-size: 16px;
  margin: 4px;
  color: #333;
  outline: none;
  cursor: pointer;
  user-select: none;
}
.current-page {
  width: 60px;
  text-align: center;
  border: none;
  border-bottom: 1px solid #ccc;
}
.pre.disabled,
.next.disabled {
  color: #ccc;
}
</style>
