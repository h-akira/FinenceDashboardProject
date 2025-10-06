<template>
  <div class="jp225-component">
    <div class="tradingview-widget-container">
      <div id="tradingview_jp225"></div>
      <div class="tradingview-widget-copyright">
        <a href="https://jp.tradingview.com/" rel="noopener nofollow" target="_blank">
          <span class="blue-text">TradingViewですべてのマーケットを追跡</span>
        </a>
      </div>
    </div>

    <div
      id="resizer"
      class="resizer"
      @mousedown="startResize">
    </div>
  </div>
</template>

<script>
export default {
  name: 'JP225',
  data() {
    return {
      currentHeight: 700,
      widget: null,
      isResizing: false
    }
  },
  mounted() {
    this.loadTradingViewScript()
  },
  methods: {
    loadTradingViewScript() {
      if (window.TradingView) {
        this.createWidget()
        return
      }

      const script = document.createElement('script')
      script.src = 'https://s3.tradingview.com/tv.js'
      script.async = true
      script.onload = () => {
        this.createWidget()
      }
      document.head.appendChild(script)
    },

    createWidget() {
      if (this.widget) {
        this.widget.remove()
      }

      this.widget = new TradingView.widget({
        width: '100%',
        height: this.currentHeight,
        symbol: 'OANDA:JP225USD',
        interval: 'D',
        timezone: 'Asia/Tokyo',
        theme: 'light',
        style: '1',
        locale: 'ja',
        enable_publishing: false,
        allow_symbol_change: true,
        container_id: 'tradingview_jp225'
      })
    },

    updateWidget() {
      this.createWidget()
    },

    startResize() {
      this.isResizing = true
      document.addEventListener('mousemove', this.resize)
      document.addEventListener('mouseup', this.stopResize)
    },

    resize(event) {
      if (!this.isResizing) return

      const container = document.querySelector('.tradingview-widget-container')
      const rect = container.getBoundingClientRect()
      const newHeight = event.clientY - rect.top

      if (newHeight > 300 && newHeight < 1200) {
        this.currentHeight = newHeight
        this.updateWidget()
      }
    },

    stopResize() {
      this.isResizing = false
      document.removeEventListener('mousemove', this.resize)
      document.removeEventListener('mouseup', this.stopResize)
    }
  },

  beforeUnmount() {
    if (this.widget) {
      this.widget.remove()
    }
    document.removeEventListener('mousemove', this.resize)
    document.removeEventListener('mouseup', this.stopResize)
  }
}
</script>

<style scoped>
.resizer {
  height: 10px;
  background: #ccc;
  cursor: ns-resize;
  margin: 10px 0;
}

.resizer:hover {
  background: #999;
}
</style>
