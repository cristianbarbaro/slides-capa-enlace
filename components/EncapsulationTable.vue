<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  mode: {
    type: String,
    default: 'request',
  },
  stage: {
    type: Number,
    default: 0,
  },
})

const requestEthernetFields = [
  { label: 'MAC destino', value: 'FF:FF:FF:FF:FF:FF (broadcast)', step: 0 },
  { label: 'MAC origen', value: 'MAC_PC-A_eth0', step: 1 },
]

const replyEthernetFields = [
  { label: 'MAC destino', value: 'MAC_PC-A_eth0 (unicast)', step: 0 },
  { label: 'MAC origen', value: 'MAC_DNS_eth0', step: 1 },
]

const requestArpFields = [
  { label: 'MAC origen (SHA)', value: 'MAC_PC-A_eth0', step: 2 },
  { label: 'IP origen (SPA)', value: '172.20.10.12 (PC-A)', step: 3 },
  { label: 'MAC destino (THA)', value: '00:00:00:00:00:00 (desconocida)', step: 4 },
  { label: 'IP destino (TPA)', value: '172.20.10.14 (DNS_Server)', step: 5 },
]

const replyArpFields = [
  { label: 'MAC origen (SHA)', value: 'MAC_DNS_eth0', step: 2 },
  { label: 'IP origen (SPA)', value: '172.20.10.14 (DNS_Server)', step: 3 },
  { label: 'MAC destino (THA)', value: 'MAC_PC-A_eth0', step: 4 },
  { label: 'IP destino (TPA)', value: '172.20.10.12 (PC-A)', step: 5 },
]

const ethernetFields = computed(() => props.mode === 'reply' ? replyEthernetFields : requestEthernetFields)
const arpFields = computed(() => props.mode === 'reply' ? replyArpFields : requestArpFields)

function isComplete(step?: number) {
  return step === undefined || props.stage > step
}

function cellStyle(step?: number) {
  return props.stage === step
    ? { border: '3px solid #d33', background: '#fff1f0', padding: '0.45em 0.7em' }
    : {}
}
</script>

<template>
  <table class="encapsulation-table" style="width: 100%; table-layout: fixed;">
    <colgroup>
      <col style="width: 34%;">
      <col style="width: 12%;">
      <col style="width: 54%;">
    </colgroup>
    <thead>
      <tr><th colspan="3"><b>Trama Ethernet</b></th></tr>
    </thead>
    <tbody>
      <tr v-for="field in ethernetFields" :key="field.label">
        <th>{{ field.label }}</th>
        <td colspan="2" :style="cellStyle(field.step)">
          <code>{{ isComplete(field.step) ? field.value : '???' }}</code>
        </td>
      </tr>
      <tr>
        <th><b>Mensaje ARP encapsulado</b></th>
        <td colspan="2">
          <table style="width: 100%; table-layout: fixed;">
            <colgroup>
              <col style="width: 48%;">
              <col style="width: 52%;">
            </colgroup>
            <tbody>
              <tr v-for="field in arpFields" :key="field.label">
                <th>{{ field.label }}</th>
                <td :style="cellStyle(field.step)">
                  <code>{{ isComplete(field.step) ? field.value : '???' }}</code>
                </td>
              </tr>
            </tbody>
          </table>
        </td>
      </tr>
    </tbody>
  </table>
</template>