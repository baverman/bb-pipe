<script setup lang="ts">
import { ref } from 'vue'
import ToggleArrow from './ToggleArrow.vue'
import Activated from './Activated.vue'
import LogContent from './LogContent.vue'
import { type Log } from '../types'

const props = defineProps<{ log: Log }>()
const details = ref(false)
</script>

<template>
    <div>
        <div
            :class="{ log: 1, 'w-100': 1, 'log-active': details, cbox: 1 }"
            @click="details = !details"
        >
            <div><ToggleArrow :active="details" />&nbsp;{{ props.log.name }}</div>
            <div class="cbox-push">
                <a
                    @click.stop=""
                    :href="`/api/v2/logs/${props.log.logid}/raw?_download=0`"
                    target="_blank"
                    >view</a
                >
                <template v-if="props.log.type != 'h'">
                    &nbsp;
                    <a
                        @click.stop=""
                        :href="`/api/v2/logs/${props.log.logid}/raw`"
                        class="log-button-small"
                    >
                        <i class="fa fa-download" aria-hidden="true"></i>&nbsp;download
                    </a>
                </template>
            </div>
        </div>
        <activated :active="details">
            <log-content v-show="details" :log="props.log" />
        </activated>
    </div>
</template>

<style>
.log {
    padding: 0.5em 0.8em;
    background-color: #f5f5f5;
    border-color: #ddd;
    border-radius: 3px;
    border-width: 1px;
    border-style: solid;
}

.log-active {
    border-radius: 3px 3px 0 0;
}

.log-button-small {
    font-size: 80%;
    padding: 0.1em 0.5em;
    border-radius: 2px;
    min-width: 4em;
    background-color: #fff;
    border: 1px solid #ccc;
    text-decoration: none;
}
</style>
