<template>
  <header>
    <div
      class="mt-2 justify-between mt-5 sm:mt-6 sm:grid sm:grid-flow-row-dense sm:grid-cols-2 sm:gap-3"
    >
      <h2>Vue</h2>
      <input
        type="text"
        name="name"
        id="name"
        class="block rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        placeholder="Login Name:Mounika"
      />
    </div>
  </header>
  <div class="justify-between mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
    <input
      type="search"
      name="name"
      id="name"
      class="block rounded-full border-0 px-4 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
      placeholder="Search"
    />

    <button
      type="button"
      @click="opensidebar()"
      class="block rounded-md align item-center bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
    >
      Add Student
    </button>
  </div>
  <CollectionAdd v-if="open" :open="open" @postData="postData"></CollectionAdd>
  <CollectionList
    v-if="templateData?.length"
    :templateData="templateData"
    @deleteData="setDeleteData"
    :edit="edit"
    @editData="updatetemplateData"
    :key="templateData"
  ></CollectionList>
  <CollectionEdit
    v-if="edit"
    :editData="editData"
    :edit="edit"
    @savedata="postData"
    :key="editData"
  ></CollectionEdit>

  <CollectionDelete
    v-if="isDelete"
    :deletedata="isDelete"
    @confirmDelete="deleteData"
    @cancelDelete="isDelete = false"
  ></CollectionDelete>
</template>
<script setup>
// Define ref
const open = ref(false);
const templateData = ref([]);
const edit = ref(false);
const isDelete = ref(false);
const editData = ref({});
const deleteDatail = ref({});

onMounted(() => {
  const items = localStorage.getItem("List");
  templateData.value = items ? JSON.parse(items) || [] : [];
});

// Post data
const postData = (form) => {
  if (editData.value && Object.keys(editData.value).length) {
    // Update existing entry
    const index = templateData.value.findIndex(
      (item) => item.id === editData.value.id
    );
    if (index !== -1) {
      templateData.value.splice(index, 1, form); // Replace the item
    }
  } else {
    // Add new entry
    templateData.value.push(form);
  }

  // Save to localStorage
  localStorage.setItem("List", JSON.stringify(templateData.value));
  edit.value = false; // Trigger edit mode

  // Reset edit mode
  editData.value = {};
  getUserData();
};

// Get data
const getUserData = () => {
  let userList = localStorage.getItem("List");
  templateData.value = JSON.parse(userList);
};

// Open sidebar
const opensidebar = () => {
  open.value = !open.value;
};

// Edit existing data (pre-fill the form)
const updatetemplateData = (item) => {
  edit.value = true; // Trigger edit mode
  editData.value = { ...item }; // Prefill edit form with selected item
};

// Delete data from templateData
const deleteData = () => {
  isDelete.value = false;
  // Find the index of the item to delete using `number`
  const index = templateData.value.findIndex(
    (item) => item.number === deleteDatail.value.number
  );
  if (index !== -1) {
    templateData.value.splice(index, 1); // Remove the item from the array
  }

  // Save updated data to localStorage
  localStorage.setItem("List", JSON.stringify(templateData.value));
  getUserData(); // Refresh the data
};

// Set delete data
const setDeleteData = (data) => {
  isDelete.value = true;
  deleteDatail.value = data;
};
</script>
