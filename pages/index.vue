<script lang="ts" setup>
import {ICard, IColumn} from "~/components/kanban/kanban.types";

useSeoMeta({
  title: "Home | CRM system"
})

const dragCard = ref<ICard | null>(null)
const sourceColumn = ref<IColumn | null>(null)


</script>

<template>
  <div class="p-10">
    <h1 class="font-bold text-2xl mb-10">CRM System by AS-GROOP</h1>
    <UiCard class="mb-3" draggable="true">
      <UiCardHeader role="button"> name card</UiCardHeader>
      <UiCardContent>Company</UiCardContent>
      <UiCardFooter>Date</UiCardFooter>
    </UiCard>
  </div>
</template>
