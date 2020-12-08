<template>
    <div id="container" v-if="!!tabs.length">
        <div 
            v-for="(tab, index) in tabs" :key="tab.id"
            class="tab-item">
            <div
                class="tab"
                :class="activeTab === index ? 'selected' : activeTab > index && clickToGo ? 'deselected selectable' : 'deselected'"
                @click="changeTabIndex(index)">
                {{tab}}
            </div>
            <span class="brace" v-if="!!tabs[index + 1]">
                >>
            </span>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        tabs: {
            type: Array,
            default: () => [],
            required: true
        },
        value: {
            default: 0,

        },
        clickToGo: {
            default: true
        }
    },
    computed: {
        activeTab: {
            get() { 
                if(this.value > this.tabs.length - 1) {
                    this.$emit('input', this.tabs.length - 1)
                    return this.tabs.length - 1
                } else if(this.value < 0) {
                    this.$emit('input', 0)
                    return 0
                } else return this.value
            },
            set(val) {
                if(val > this.tabs.length - 1) this.$emit('input', this.tabs.length - 1)
                else if(val < 0) this.$emit('input', 0)
                else this.$emit('input', val )
            }
        }
    },
    methods: {
        nextTab() { 
            console.log('+++')
            this.activeTab++
        },
        previousTab() {
            console.log('---')
            this.activeTab--
        },
        changeTabIndex(index) {
            console.log('cccc')
            if(!this.clickToGo || this.value <= index) return
            this.activeTab = index
        }
    }
}
</script>

<style scoped>
#container {
    width: min-content;
    background: white;
    padding: 10px;
    border-radius: 10px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-start;
}
.tab {
    padding: 10px;
}
.tab-item {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
}
.brace {
    margin-left: 10px;
    margin-right: 10px;
}
.selected {
    transition: all .1s;
    border-bottom: 1px solid #7367F0;
    color: #7367F0;
    cursor: default;
}
.deselected {
    transition: all .2s;
    color: #CCCCCC;
    cursor: default;
}
.selectable {
    cursor: pointer;
    color: gray;
}
.selectable:hover {
    background: #D5DAE0;
    color: gray;
}
.fade-enter-active,
.fade-leave-active {
    transition: opacity .5s
}

.fade-enter,
.fade-leave-to {
    opacity: 0
}
</style>