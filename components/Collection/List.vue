<template>
  <scetion>
    <div class="px-4 sm:px-6 lg:px-8">
      <div class="sm:flex sm:items-center">
        <div class="sm:flex-auto"></div>
      </div>
      <div class="mt-8 flow-root">
        <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
          <div
            class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8"
          >
            <div
              class="overflow-hidden shadow ring-1 ring-black ring-opacity-5 sm:rounded-lg"
            >
              <table class="min-w-full divide-y divide-gray-300">
                <thead class="bg-gray-50">
                  <tr>
                    <th
                      scope="col"
                      class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6"
                    >
                      S.No
                    </th>
                    <th
                      scope="col"
                      class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6"
                    >
                      Name
                    </th>
                    <th
                      scope="col"
                      class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                    >
                      Age
                    </th>
                    <th
                      scope="col"
                      class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                    >
                      Gender
                    </th>
                    <th
                      scope="col"
                      class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                    >
                      DateOfBirth
                    </th>
                    <th
                      scope="col"
                      class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                    >
                      Class
                    </th>
                    <th
                      scope="col"
                      class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                    >
                      Actions
                    </th>
                    <th
                      scope="col"
                      class="relative py-3.5 pl-3 pr-4 sm:pr-6"
                    ></th>
                  </tr>
                </thead>

                <tbody
                  class="divide-y divide-gray-200 bg-white"
                  v-if="templateData?.length"
                >
                  <tr v-for="template in templateData" :key="template.number">
                    <td
                      class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-6"
                    >
                      {{ template.number }}
                    </td>
                    <td
                      class="whitespace-nowrap px-3 py-4 text-sm text-gray-500"
                    >
                      {{ template.Name }}
                    </td>
                    <td
                      class="whitespace-nowrap px-3 py-4 text-sm text-gray-500"
                    >
                      {{ template.Age }}
                    </td>
                    <td
                      class="whitespace-nowrap px-3 py-4 text-sm text-gray-500"
                    >
                      {{ template.Gender }}
                    </td>
                    <td
                      class="whitespace-nowrap px-3 py-4 text-sm text-gray-500"
                    >
                      {{ template.DateOfBirth }}
                    </td>
                    <td
                      class="whitespace-nowrap px-3 py-4 text-sm text-gray-500"
                    >
                      {{ template.Class }}
                    </td>
                    <td
                      class="whitespace-nowrap px-3 py-4 text-sm text-gray-500"
                    >
                      {{ template.Actions }}
                    </td>
                    <td class="px-4 py-2">
                      <div class="align item-center justify-between">
                        <PencilSquareIcon
                          name="iconoir:edit-pencil"
                          size="20"
                          class="h-5 w-5 flex-shrink-0 text-gray-400 group-hover:text-gray-500"
                          @click="editData(template)"
                        >
                        </PencilSquareIcon>
                        <TrashIcon
                          name="bytesize:trash"
                          size="16"
                          class="h-5 w-5 flex-shrink-0 text-gray-400 group-hover:text-gray-500:text-red-600"
                          @click="deleteData(template)"
                        >
                        </TrashIcon>
                      </div>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
  </scetion>
</template>
<script setup>
import { PlusIcon, PencilSquareIcon, TrashIcon } from "@heroicons/vue/20/solid";

//define the props
const props = defineProps({
  templateData: Array,
});

//define the emits
const emits = defineEmits(["editData", "deleteData"]);

//emits the edit data
const editData = (items) => {
  emits("editData", items);
};

//emits the delete data
const deleteData = (data) => {
  emits("deleteData", data);
};
</script>
