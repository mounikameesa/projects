<template>
  <TransitionRoot as="template" :show="edit">
    <Dialog as="div" class="relative z-10" @close="edit = false">
      <TransitionChild
        as="template"
        enter="ease-out duration-300"
        enter-from="opacity-0"
        enter-to="opacity-100"
        leave="ease-in duration-200"
        leave-from="opacity-100"
        leave-to="opacity-0"
      >
        <div
          class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"
        />
      </TransitionChild>

      <div class="fixed inset-0 z-10 overflow-y-auto">
        <div
          class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0"
        >
          <TransitionChild
            as="template"
            enter="ease-out duration-300"
            enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            enter-to="opacity-100 translate-y-0 sm:scale-100"
            leave="ease-in duration-200"
            leave-from="opacity-100 translate-y-0 sm:scale-100"
            leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
          >
            <DialogPanel
              class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6"
            >
              <div class="justify-between">
                <div>
                  <label
                    for="number"
                    class="block text-sm font-medium leading-6 text-gray-900"
                    >S.No</label
                  >
                  <input
                    type="number"
                    name="number"
                    id="number"
                    v-model="editData.number"
                    class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                  />
                </div>
                <div>
                  <label
                    for="text"
                    class="block text-sm font-medium leading-6 text-gray-900"
                    >Name</label
                  >
                  <input
                    type="text"
                    name="text"
                    id="text"
                    v-model="editData.Name"
                    class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                  />
                </div>
                <div>
                  <label
                    for="number"
                    class="block text-sm font-medium leading-6 text-gray-900"
                    >Age</label
                  >
                  <input
                    type="number"
                    name="number"
                    id="number"
                    v-model="editData.Age"
                    class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                  />
                </div>
                <div>
                  <label
                    for="Gender"
                    class="block text-sm font-medium leading-6 text-gray-900"
                    >Gender</label
                  >
                  <select
                    id="Gender"
                    name="Gender"
                    v-model="editData.Gender"
                    class="mt-2 block w-full rounded-md border-0 py-1.5 pl-3 pr-10 text-gray-900 ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-indigo-600 sm:text-sm sm:leading-6"
                  >
                    <option>Male</option>
                    <option selected="">Female</option>
                  </select>
                </div>
                <div>
                  <label
                    for="text"
                    class="block text-sm font-medium leading-6 text-gray-900"
                    >DateOfBirth</label
                  >
                  <input
                    type="text"
                    name="text"
                    id="text"
                    v-model="editData.DataOfBirth"
                    class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                  />
                </div>
                <div>
                  <label
                    for="Class"
                    class="block text-sm font-medium leading-6 text-gray-900"
                    >Class</label
                  >
                  <select
                    id="Class"
                    v-model="editData.Class"
                    name="Class"
                    class="mt-2 block w-full rounded-md border-0 py-1.5 pl-3 pr-10 text-gray-900 ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-indigo-600 sm:text-sm sm:leading-6"
                  >
                    <option>First Year</option>
                    <option>Second Year</option>
                    <option selected="">Inter</option>
                  </select>
                </div>
              </div>
              <div
                class="mt-5 sm:mt-6 sm:grid sm:grid-flow-row-dense sm:grid-cols-2 sm:gap-3"
              >
                <div @click="edit = false">
                  <button
                    type="button"
                    @click="saveFormData()"
                    class="inline-flex w-full justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2"
                  >
                    Update
                  </button>
                </div>
                <button
                  type="button"
                  class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                  @click="edit = false"
                  ref="cancelButtonRef"
                >
                  Cancel
                </button>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>
<script setup>
import {
  Dialog,
  DialogPanel,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";

const emit = defineEmits(["savedata"]);
const props = defineProps({
  edit: Boolean,
  editData: Object,
});
const editData = ref(props.editData);

const saveFormData = () => {
  emit("savedata", editData.value);
  editData.value = {};
};
</script>
