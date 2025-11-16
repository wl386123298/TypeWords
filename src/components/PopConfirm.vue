<script lang="jsx">
import {Teleport, Transition} from 'vue'
import BaseButton from "@/components/BaseButton.vue";

export default {
  name: "PopConfirm",
  components: {
    Teleport,
    Transition,
    BaseButton
  },
  props: {
    title: {
      type: String,
      default() {
        return ''
      }
    },
    disabled: {
      type: Boolean,
      default() {
        return false
      }
    }
  },
  data() {
    return {
      show: false
    }
  },
  mounted() {
    window.addEventListener('click', () => {
      this.show = false
    })
    window.addEventListener('keydown', () => {
      this.show = false
    })
  },
  methods: {
    showPop(e) {
      if (this.disabled) return this.$emit('confirm')
      e?.stopPropagation()
      let rect = e.target.getBoundingClientRect()
      this.show = true
      this.$nextTick(() => {
        let tip = this.$refs?.tip?.getBoundingClientRect()
        // console.log('rect', rect, tip)
        if (!tip) return
        if (rect.top < 150) {
          this.$refs.tip.style.top = rect.top + rect.height + tip.height + 30 + 'px'
        } else {
          this.$refs.tip.style.top = rect.top - 10 + 'px'
        }
        this.$refs.tip.style.left = rect.left + rect.width / 2 - 50 + 'px'
      })
    },
    confirm() {
      this.show = false
      this.$emit('confirm')
    }
  },
  render() {
    let Vnode = this.$slots.default()[0]
    return (
        <div class="pop-confirm leading-none">
          <Teleport to="body">
            <Transition name="fade">
              {
                  this.show && (
                      <div ref="tip" class="pop-confirm-content shadow-2xl">
                        <div class="w-50">
                          {this.title}
                        </div>
                        <div class="options">
                          <BaseButton type="info" size="small" onClick={() => this.show = false}>取消</BaseButton>
                          <BaseButton size="small" onClick={() => this.confirm()}>确认</BaseButton>
                        </div>
                      </div>
                  )
              }
            </Transition>
          </Teleport>
          <Vnode onClick={(e) => this.showPop(e)}/>
        </div>
    )
  }
}
</script>
<style lang="scss" scoped>
.pop-confirm-content {
  position: fixed;
  background: var(--color-tooltip-bg);
  padding: 1rem;
  border-radius: .6rem;
  transform: translate(-50%, calc(-100% - .6rem));
  z-index: 999;


  .options {
    margin-top: .9rem;
    text-align: right;
  }
}
</style>
