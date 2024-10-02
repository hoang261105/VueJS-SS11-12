<template>
  <div class="container mx-auto p-6">
    <div class="flex justify-between items-center mb-4">
      <h2 class="text-2xl font-bold">Quản lý mượn trả sách</h2>
      <div>
        <select name="" id="">
          <option value="">Lọc theo trạng thái</option>
          <option value="true">Đã trả</option>
          <option value="false">Chưa trả</option>
        </select>
        <button
          class="bg-blue-500 hover:bg-blue-600 text-white font-semibold py-2 px-4 rounded"
          @click="handleShowForm"
        >
          Thêm thông tin
        </button>
      </div>
    </div>

    <!-- Form thêm thông tin sách -->
    <div
      v-if="showForm"
      class="fixed inset-0 flex justify-center items-center bg-black bg-opacity-50"
    >
      <div class="bg-white p-6 rounded-lg shadow-lg w-full max-w-md">
        <h3 class="text-xl font-semibold mb-4">Thêm thông tin sách</h3>
        <form @submit.prevent="handleSubmit">
          <div class="mb-4">
            <label class="block text-sm font-medium mb-2">Tên sách</label>
            <input
              type="text"
              v-model="inputValue.nameBook"
              class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
            <p class="text-red-500">{{ error.nameBook }}</p>
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-2">Người mượn</label>
            <input
              type="text"
              v-model="inputValue.fullName"
              class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
            <p class="text-red-500">{{ error.fullName }}</p>
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-2">Ngày mượn</label>
            <input
              type="date"
              v-model="inputValue.dateStart"
              class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
            <p class="text-red-500">{{ error.dateStart }}</p>
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-2">Ngày trả</label>
            <input
              type="date"
              v-model="inputValue.dateEnd"
              class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
            <p class="text-red-500">{{ error.dateEnd }}</p>
          </div>
          <div class="flex justify-end gap-2">
            <button
              type="button"
              class="bg-red-500 hover:bg-red-600 text-white font-semibold py-2 px-4 rounded-lg"
              @click="handleCloseForm"
            >
              Đóng
            </button>

            <button
              type="submit"
              class="bg-green-500 hover:bg-green-600 text-white font-semibold py-2 px-4 rounded-lg"
            >
              Lưu thông tin
            </button>
          </div>
        </form>
      </div>
    </div>

    <!-- Form sửa thông tin sách -->
    <div
      v-if="showFormEdit"
      class="fixed inset-0 flex justify-center items-center bg-black bg-opacity-50"
    >
      <div class="bg-white p-6 rounded-lg shadow-lg w-full max-w-md">
        <h3 class="text-xl font-semibold mb-4">Sửa thông tin sách</h3>
        <form @submit.prevent="handleEdit">
          <div class="mb-4">
            <label class="block text-sm font-medium mb-2">Tên sách</label>
            <input
              type="text"
              v-model="selectedBookEdit.nameBook"
              class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
            <p class="text-red-500">{{ error.nameBook }}</p>
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-2">Người mượn</label>
            <input
              type="text"
              v-model="selectedBookEdit.fullName"
              class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
            <p class="text-red-500">{{ error.fullName }}</p>
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-2">Ngày mượn</label>
            <input
              type="date"
              v-model="selectedBookEdit.dateStart"
              class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
            <p class="text-red-500">{{ error.dateStart }}</p>
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-2">Ngày trả</label>
            <input
              type="date"
              v-model="selectedBookEdit.dateEnd"
              class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            />
            <p class="text-red-500">{{ error.dateEnd }}</p>
          </div>
          <div class="flex justify-end gap-2">
            <button
              type="button"
              class="bg-red-500 hover:bg-red-600 text-white font-semibold py-2 px-4 rounded-lg"
              @click="handleCloseFormEdit"
            >
              Đóng
            </button>

            <button
              type="submit"
              class="bg-green-500 hover:bg-green-600 text-white font-semibold py-2 px-4 rounded-lg"
            >
              Cập nhật
            </button>
          </div>
        </form>
      </div>
    </div>

    <table class="min-w-full bg-white border border-gray-200">
      <thead>
        <tr>
          <th class="py-2 px-4 border-b border border-gray-300">STT</th>
          <th class="py-2 px-4 border-b border border-gray-300">Tên sách</th>
          <th class="py-2 px-4 border-b border border-gray-300">
            Sinh viên mượn
          </th>
          <th class="py-2 px-4 border-b border border-gray-300">Ngày mượn</th>
          <th class="py-2 px-4 border-b border border-gray-300">Ngày trả</th>
          <th class="py-2 px-4 border-b border border-gray-300">Trạng thái</th>
          <th class="py-2 px-4 border-b border border-gray-300">Chức năng</th>
        </tr>
      </thead>

      <tbody>
        <!-- Dòng 1 -->
        <tr v-for="(book, index) in filteredBooks" :key="book.id">
          <td class="py-2 px-4 border-b border border-gray-300 text-center">
            {{ index + 1 }}
          </td>
          <td class="py-2 px-4 border-b border border-gray-300 text-center">
            {{ book.nameBook }}
          </td>
          <td class="py-2 px-4 border-b border border-gray-300 text-center">
            {{ book.fullName }}
          </td>
          <td class="py-2 px-4 border-b border border-gray-300 text-center">
            {{ book.dateStart }}
          </td>
          <td class="py-2 px-4 border-b border border-gray-300 text-center">
            {{ book.dateEnd }}
          </td>
          <td class="py-2 px-4 border-b border border-gray-300 text-center">
            <span
              :class="
                book.status === false
                  ? 'bg-red-500 text-white px-2 py-1 rounded'
                  : 'bg-green-400 text-white px-2 py-1 rounded'
              "
              >{{ book.status === false ? "Chưa trả" : "Đã trả" }}</span
            >
          </td>
          <td class="py-2 px-4 border-b border border-gray-300 text-center">
            <button
              class="bg-yellow-400 hover:bg-yellow-500 text-white font-semibold py-1 px-3 rounded"
              @click="handleShowEdit(book)"
            >
              Sửa
            </button>
            <button
              class="bg-red-500 hover:bg-red-600 text-white font-semibold py-1 px-3 rounded ml-2"
              @click="handleShowConFirm(book.id)"
            >
              Xóa
            </button>
          </td>
        </tr>
      </tbody>
    </table>

    <div
      v-if="showDeleteModal"
      class="fixed inset-0 flex justify-center items-center bg-black bg-opacity-50"
    >
      <div class="bg-white p-6 rounded-lg shadow-lg w-full max-w-md">
        <h3 class="text-xl font-semibold mb-4">Xác nhận xóa thông tin</h3>
        <p>Bạn có chắc chắn muốn xóa thông tin sách này?</p>
        <div class="flex justify-end gap-2 mt-4">
          <button
            class="bg-gray-500 hover:bg-gray-600 text-white font-semibold py-2 px-4 rounded-lg"
            @click="handleCloseDeleteModal"
          >
            Hủy
          </button>
          <button
            class="bg-red-500 hover:bg-red-600 text-white font-semibold py-2 px-4 rounded-lg"
            @click="handleDelete"
          >
            Xóa
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, reactive, ref } from "vue";
const showForm = ref(false);
const showFormEdit = ref(false);
const showDeleteModal = ref(false);
const selectedBook = ref(null);
const selectedBookEdit = ref(null);
const filterStatus = ref("");
let listBooks = reactive(JSON.parse(localStorage.getItem("listBooks")) || []);
const inputValue = reactive({
  nameBook: "",
  fullName: "",
  dateStart: "",
  dateEnd: "",
});

const error = reactive({
  nameBook: "",
  fullName: "",
  dateStart: "",
  dateEnd: "",
});

const handleShowForm = () => {
  showForm.value = !showForm.value;
};

const handleCloseForm = () => {
  showForm.value = false;
};

const saveToLocal = (key, value) => {
  localStorage.setItem(key, JSON.stringify(value));
};

const handleSubmit = () => {
  const dateToStart = new Date(inputValue.dateStart);
  const dateToEnd = new Date(inputValue.dateEnd);
  const currentDate = new Date();
  if (!inputValue.nameBook) {
    error.nameBook = "Vui lòng nhập tên sách";
  } else {
    error.nameBook = "";
  }

  if (!inputValue.fullName) {
    error.fullName = "Vui lòng nhập tên tác giả";
  } else {
    error.fullName = "";
  }

  if (!inputValue.dateStart) {
    error.dateStart = "Vui lòng nhập ngày mượn";
  } else if (dateToStart < currentDate) {
    error.dateStart = "Ngày mượn không được bé hơn ngày hiện tại";
  } else {
    error.dateStart = "";
  }

  if (!inputValue.dateEnd) {
    error.dateEnd = "Vui lòng nhập ngày mượn";
  } else if (dateToEnd < currentDate) {
    error.dateEnd = "Ngày trả không được bé hơn ngày hiện tại";
  } else {
    error.dateEnd = "";
  }

  if (
    !error.nameBook &&
    !error.fullName &&
    !error.dateStart &&
    !error.dateEnd
  ) {
    const newBook = {
      id: Math.ceil(Math.random() * 10000),
      nameBook: inputValue.nameBook,
      fullName: inputValue.fullName,
      status: false,
      dateStart: inputValue.dateStart,
      dateEnd: inputValue.dateEnd,
    };
    listBooks.push(newBook);
    saveToLocal("listBooks", listBooks);
    showForm.value = false;
    inputValue.nameBook = "";
    inputValue.fullName = "";
    inputValue.dateStart = "";
    inputValue.dateEnd = "";
  }
};

// Hàm xóa sách
const handleShowConFirm = (bookId) => {
  selectedBook.value = bookId;
  showDeleteModal.value = true;
};

const handleCloseDeleteModal = () => {
  showDeleteModal.value = false;
};

const handleDelete = () => {
  listBooks = listBooks.filter((item) => item.id !== selectedBook.value);
  saveToLocal("listBooks", listBooks);
  showDeleteModal.value = false;
};

// Hàm sửa thông tin sách
const handleShowEdit = (book) => {
  selectedBookEdit.value = book;
  showFormEdit.value = true;
};

const handleEdit = () => {
  const dateToStart = new Date(selectedBookEdit.value.dateStart);
  const dateToEnd = new Date(selectedBookEdit.value.dateEnd);
  const currentDate = new Date();
  if (!selectedBookEdit.value.nameBook) {
    error.nameBook = "Vui lòng nhập tên sách";
  } else {
    error.nameBook = "";
  }

  if (!selectedBookEdit.value.fullName) {
    error.fullName = "Vui lòng nhập tên tác giả";
  } else {
    error.fullName = "";
  }

  if (!selectedBookEdit.value.dateStart) {
    error.dateStart = "Vui lòng nhập ngày mượn";
  } else if (dateToStart < currentDate) {
    error.dateStart = "Ngày mượn không được bé hơn ngày hiện tại";
  } else {
    error.dateStart = "";
  }

  if (!selectedBookEdit.value.dateEnd) {
    error.dateEnd = "Vui lòng nhập ngày mượn";
  } else if (dateToEnd < currentDate) {
    error.dateEnd = "Ngày trả không được bé hơn ngày hiện tại";
  } else {
    error.dateEnd = "";
  }

  if (
    !error.nameBook &&
    !error.fullName &&
    !error.dateStart &&
    !error.dateEnd
  ) {
    const bookUpdateIndex = listBooks.findIndex(
      (book) => book.id === selectedBookEdit.value.id
    );
    if (bookUpdateIndex !== -1) {
      listBooks[bookUpdateIndex] = { ...selectedBookEdit.value };
      saveToLocal("listBooks", listBooks);
      showFormEdit.value = false;
    }
  }
};

const handleCloseFormEdit = () => {
  showFormEdit.value = false;
};

// Hàm lọc
const filteredBooks = computed(() => {
  if (filterStatus.value === "") {
    return listBooks;
  }
  return listBooks.filter((book) => String(book.status) === filterStatus.value);
});
</script>

<style></style>
