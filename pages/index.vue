<template>
  <div>
    <VCard class="filter-dropdown">
      <AppSelect
        :items="items"
        density="compact"
        placeholder="Khu vực"
      />
      <AppSelect
        :items="items"
        density="compact"
        placeholder="Nguồn"
      />
      <AppSelect
        :items="items"
        density="compact"
        placeholder="Loại nhà"
      />
      <AppSelect
        :items="items"
        density="compact"
        placeholder="Loại giao dịch"
      />
      <VBtn
        variant="flat"
        color="secondary"
      >
        Xoá lọc
      </VBtn>
      <VBtn variant="flat">
        Lọc
      </VBtn>
    </VCard>

    <VCard class="table-info-display">
      <div class="filter-table-date-name">
        <AppTextField class="filter-text-field"
                      density="compact"
                      placeholder="Tìm kiếm theo địa chỉ hoặc tên người đăng"
        />
        <AppDateTimePicker
          v-model="dateRange"
          prepend-inner-icon="tabler-archive"
          placeholder="Select date"
          :config="{ mode: 'range', showMonths: 2 }"
        />
      </div>
      <div class="info-header">
        <div class="display-info-number note">
          <div>Chưa chọn</div>
          <span>3024</span>
        </div>
        <div class="display-info-number">
          <div>Đã chọn</div>
          <span>30</span>
        </div>
        <div class="display-info-number">
          <div>Không chọn</div>
          <span>3024</span>
        </div>
      </div>
      <VDataTable
        :headers="headers"
        :items="data"
        :items-per-page="10"
      >
        <!-- Type -->
        <template #item.type="{ item }">
          <div class="d-flex align-center">
            <div class="item-type d-flex flex-column">
              <div class="house-type-acreage">{{ item.type }}</div>
              <span class="house-adress">{{ item.address }}</span>
              <nuxt-link :to="`/`" class="link-source">
                {{ item.source }}
                <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 12 12" fill="none">
                  <path
                    d="M5.5 3.5H3C2.44772 3.5 2 3.94772 2 4.5V9C2 9.55228 2.44772 10 3 10H7.5C8.05228 10 8.5 9.55228 8.5 9V6.5"
                    stroke="#4B465C" stroke-width="0.920455" stroke-linecap="round" stroke-linejoin="round"/>
                  <path
                    d="M5.5 3.5H3C2.44772 3.5 2 3.94772 2 4.5V9C2 9.55228 2.44772 10 3 10H7.5C8.05228 10 8.5 9.55228 8.5 9V6.5"
                    stroke="white" stroke-opacity="0.5" stroke-width="0.920455" stroke-linecap="round"
                    stroke-linejoin="round"/>
                  <path d="M5 7L10 2" stroke="#4B465C" stroke-width="0.920455" stroke-linecap="round"
                        stroke-linejoin="round"/>
                  <path d="M5 7L10 2" stroke="white" stroke-opacity="0.5" stroke-width="0.920455" stroke-linecap="round"
                        stroke-linejoin="round"/>
                  <path d="M7.5 2H10V4.5" stroke="#4B465C" stroke-width="0.920455" stroke-linecap="round"
                        stroke-linejoin="round"/>
                  <path d="M7.5 2H10V4.5" stroke="white" stroke-opacity="0.5" stroke-width="0.920455"
                        stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              </nuxt-link>
            </div>
          </div>
        </template>

        <!-- Status -->
        <template #item.status="{ item }">
          <VChip
            :color="resolveStatusVariant(item.status).color"
            class="font-weight-medium"
            size="small"
          >
            {{ resolveStatusVariant(item.status).text }}
          </VChip>
        </template>

        <!-- Sale Type -->
        <template #item.saleType="{ item }">
          <div class="sale-type">{{item.saleType}}</div>
        </template>

        <!-- Price -->
        <template #item.salary="{ item }">
          <div class="item-salary">{{item.salary}}</div>
        </template>

        <!-- full name -->
        <template #item.fullName="{ item }">
          <div class="d-flex align-center">
            <div class="item-fullName d-flex flex-column">
              <div class="author-name">{{ item.fullName }}</div>
              <span class="total-post">{{ item.totalPost }}</span>
            </div>
          </div>
        </template>

        <!-- Actions -->
        <template #item.actions="{ item }">
          <div class="d-flex gap-1 item-action">
            <IconBtn class="accept-btn">
              <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 22 22" fill="none">
                <path d="M4.58331 11L9.16665 15.5833L18.3333 6.41666" stroke="#28C76F" stroke-width="1.5"
                      stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M4.58331 11L9.16665 15.5833L18.3333 6.41666" stroke="black" stroke-opacity="0.25"
                      stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
              </svg>
            </IconBtn>
            <IconBtn class="delete-btn" @click="deleteItem(item.raw)">
              <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 22 22" fill="none">
                <path d="M16.5 5.5L5.5 16.5" stroke="#EA5455" stroke-width="1.5" stroke-linecap="round"
                      stroke-linejoin="round"/>
                <path d="M5.5 5.5L16.5 16.5" stroke="#EA5455" stroke-width="1.5" stroke-linecap="round"
                      stroke-linejoin="round"/>
              </svg>
            </IconBtn>
            <IconBtn>
              <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 22 22" fill="none">
                <circle cx="11" cy="11" r="0.916667" stroke="#4B465C" stroke-width="1.5" stroke-linecap="round"
                        stroke-linejoin="round"/>
                <circle cx="11" cy="11" r="0.916667" stroke="white" stroke-opacity="0.2" stroke-width="1.5"
                        stroke-linecap="round" stroke-linejoin="round"/>
                <circle cx="11" cy="17.4167" r="0.916667" stroke="#4B465C" stroke-width="1.5" stroke-linecap="round"
                        stroke-linejoin="round"/>
                <circle cx="11" cy="17.4167" r="0.916667" stroke="white" stroke-opacity="0.2" stroke-width="1.5"
                        stroke-linecap="round" stroke-linejoin="round"/>
                <ellipse cx="11" cy="4.58332" rx="0.916667" ry="0.916667" stroke="#4B465C" stroke-width="1.5"
                         stroke-linecap="round" stroke-linejoin="round"/>
                <ellipse cx="11" cy="4.58332" rx="0.916667" ry="0.916667" stroke="white" stroke-opacity="0.2"
                         stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
              </svg>
            </IconBtn>
          </div>
        </template>
      </VDataTable>
    </VCard>
  </div>

  <!-- 👉 Delete Dialog  -->
  <VDialog
    v-model="deleteDialog"
    max-width="500px"
  >
    <VCard>
      <VCardTitle>
        Are you sure you want to delete this item?
      </VCardTitle>

      <VCardActions>
        <VSpacer/>

        <VBtn
          color="error"
          variant="outlined"
          @click="closeDelete"
        >
          Cancel
        </VBtn>

        <VBtn
          color="success"
          variant="elevated"
          @click="deleteItemConfirm"
        >
          OK
        </VBtn>

        <VSpacer/>
      </VCardActions>
    </VCard>
  </VDialog>
</template>

<script setup>
const dateRange = ref('')
const items = [
  'Foo',
  'Bar',
  'Fizz',
  'Buzz',
]

import {VDataTable} from 'vuetify/labs/VDataTable'
//import data from '@/views/demos/forms/tables/data-table/datatable'

const editDialog = ref(false)
const deleteDialog = ref(false)

const defaultItem = ref({
  responsiveId: '',
  id: -1,
  avatar: '',
  fullName: '',
  post: '',
  email: '',
  city: '',
  startDate: '',
  salary: -1,
  age: '',
  experience: '',
  status: -1,
})

const editedItem = ref(defaultItem.value)
const editedIndex = ref(-1)
const userList = ref([])

const headers = [
  {
    title: 'ID',
    key: 'id',
  },
  {
    title: 'Tiêu đề',
    key: 'type',
  },
  {
    title: 'Trạng thái',
    key: 'status',
  },
  {
    title: 'Loại',
    key: 'saleType',
  },
  {
    title: 'Giá',
    key: 'salary',
  },
  {
    title: 'Người đăng',
    key: 'fullName',
  },
  {
    title: 'Ngày crawl',
    key: 'startDate',
  },
  {
    title: 'Hành động',
    key: 'actions',
  }
]

const data = [
  {
    id: 11231,
    fullName: 'Vũ Minh Anh Tuấn',
    type: '[Loại BĐS] - [diện tích]',
    saleType:'Cho thuê',
    address: 'An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ',
    source: 'Nguồn: batdonsan.com.vn',
    startDate: '8/12/2023',
    salary: '10,5 tr',
    age: '27',
    status: 4,
    totalPost: '12 tin',
  },
  {
    id: 11231,
    fullName: 'Vũ Minh Anh Tuấn',
    type: '[Loại BĐS] - [diện tích]',
    saleType:'Bán',
    address: 'An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ',
    source: 'Nguồn: batdonsan.com.vn',
    startDate: '8/12/2023',
    salary: '10,5 tỷ',
    age: '27',
    status: 4,
    totalPost: '12 tin',
  },
  {
    id: 11231,
    fullName: 'Vũ Minh Anh Tuấn',
    type: '[Loại BĐS] - [diện tích]',
    saleType:'Cho thuê',
    address: 'An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ',
    source: 'Nguồn: batdonsan.com.vn',
    startDate: '8/12/2023',
    salary: '10,5 tr',
    age: '27',
    status: 4,
    totalPost: '',
  },
  {
    id: 11231,
    fullName: 'Vũ Minh Anh Tuấn',
    type: '[Loại BĐS] - [diện tích]',
    saleType:'Cho thuê',
    address: 'An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ',
    source: 'Nguồn: batdonsan.com.vn',
    startDate: '8/12/2023',
    salary: '10,5 tr',
    age: '27',
    status: 4,
    totalPost: '12 tin',
  },
  {
    id: 11231,
    fullName: 'Vũ Minh Anh Tuấn',
    type: '[Loại BĐS] - [diện tích]',
    saleType:'Bán',
    address: 'An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ',
    source: 'Nguồn: batdonsan.com.vn',
    startDate: '8/12/2023',
    salary: '10,5 tỷ',
    age: '27',
    status: 4,
    totalPost: '12 tin',
  },
  {
    id: 11231,
    fullName: 'Vũ Minh Anh Tuấn',
    type: '[Loại BĐS] - [diện tích]',
    saleType:'Cho thuê',
    address: 'An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ',
    source: 'Nguồn: batdonsan.com.vn',
    startDate: '8/12/2023',
    salary: '10,5 tr',
    age: '27',
    status: 4,
    totalPost: '',
  },
  {
    id: 11231,
    fullName: 'Vũ Minh Anh Tuấn',
    type: '[Loại BĐS] - [diện tích]',
    saleType:'Cho thuê',
    address: 'An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ',
    source: 'Nguồn: batdonsan.com.vn',
    startDate: '8/12/2023',
    salary: '10,5 tr',
    age: '27',
    status: 4,
    totalPost: '12 tin',
  },
  {
    id: 11231,
    fullName: 'Vũ Minh Anh Tuấn',
    type: '[Loại BĐS] - [diện tích]',
    saleType:'Bán',
    address: 'An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ',
    source: 'Nguồn: batdonsan.com.vn',
    startDate: '8/12/2023',
    salary: '10,5 tỷ',
    age: '27',
    status: 4,
    totalPost: '12 tin',
  },
  {
    id: 11231,
    fullName: 'Vũ Minh Anh Tuấn',
    type: '[Loại BĐS] - [diện tích]',
    saleType:'Cho thuê',
    address: 'An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ',
    source: 'Nguồn: batdonsan.com.vn',
    startDate: '8/12/2023',
    salary: '10,5 tr',
    age: '27',
    status: 4,
    totalPost: '',
  },
  {
    id: 11231,
    fullName: 'Vũ Minh Anh Tuấn',
    type: '[Loại BĐS] - [diện tích]',
    saleType:'Cho thuê',
    address: 'An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ',
    source: 'Nguồn: batdonsan.com.vn',
    startDate: '8/12/2023',
    salary: '10,5 tr',
    age: '27',
    status: 4,
    totalPost: '12 tin',
  },
  {
    id: 11231,
    fullName: 'Vũ Minh Anh Tuấn',
    type: '[Loại BĐS] - [diện tích]',
    saleType:'Bán',
    address: 'An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ',
    source: 'Nguồn: batdonsan.com.vn',
    startDate: '8/12/2023',
    salary: '10,5 tỷ',
    age: '27',
    status: 4,
    totalPost: '12 tin',
  },
  {
    id: 11231,
    fullName: 'Vũ Minh Anh Tuấn',
    type: '[Loại BĐS] - [diện tích]',
    saleType:'Cho thuê',
    address: 'An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ An Dương Vương, Phường Phú Thượng, Quận Tây Hồ',
    source: 'Nguồn: batdonsan.com.vn',
    startDate: '8/12/2023',
    salary: '10,5 tr',
    age: '27',
    status: 4,
    totalPost: '',
  },
]

const resolveStatusVariant = status => {
  if (status === 1)
    return {
      color: 'primary',
      text: 'Current',
    }
  else if (status === 2)
    return {
      color: 'success',
      text: 'Professional',
    }
  else if (status === 3)
    return {
      color: 'error',
      text: 'Rejected',
    }
  else if (status === 4)
    return {
      color: 'warning',
      text: 'Chưa chọn',
    }
  else
    return {
      color: 'info',
      text: 'Applied',
    }
}

const deleteItem = item => {
  editedIndex.value = userList.value.indexOf(item)
  editedItem.value = {...item}
  deleteDialog.value = true
}
const close = () => {
  editDialog.value = false
  editedIndex.value = -1
  editedItem.value = {...defaultItem.value}
}

const closeDelete = () => {
  deleteDialog.value = false
  editedIndex.value = -1
  editedItem.value = {...defaultItem.value}
}

const deleteItemConfirm = () => {
  userList.value.splice(editedIndex.value, 1)
  closeDelete()
}

onMounted(async () => {
  const {data} = await useApi('/api/hello')
  console.log(data)
})
</script>

<style lang="scss" scoped>
.filter-dropdown {
  display: flex;
  width: 100%;
  padding: 24px;
  align-items: flex-start;
  gap: 24px;
  border-radius: 6px;
  background: var(--Light-Solid-Color-Extra-Card-Background, #FFF);
  margin-bottom: 26px;

  /* Light/Gray/Card */
  box-shadow: 0px 4px 18px 0px rgba(75, 70, 92, 0.10);
}

.table-info-display {
  display: flex;
  padding: 24px 0;
  flex-direction: column;
  align-items: flex-start;
  gap: 16px;
  align-self: stretch;

  .filter-table-date-name {
    width: 100%;
    display: flex;
    padding: 0 24px;
    align-items: flex-start;
    gap: 16px;
    align-self: stretch;
    flex-basis: 0;

    .filter-text-field, .app-picker-field {
      width: 100%;
    }


  }

  .info-header {
    display: flex;
    padding: 0 24px;
    align-items: center;
    gap: 26px;
    align-self: stretch;

    .display-info-number {
      display: flex;
      align-items: center;
      gap: 6px;
      color: var(--Light-Typography-Color-Heading-Text, #4B465C);
      font-feature-settings: 'clig' off, 'liga' off;

      /* Light/Basic Typography/H6 Heading */
      font-family: "Public Sans";
      font-size: 15px;
      font-style: normal;
      font-weight: 500;
      line-height: 21px; /* 140% */
    }

    .note {
      color: var(--Light-Solid-Color-Primary-Primary---900, #7367F0);
    }
  }

  .item-type{
    padding: 11px 0;
    .house-type-acreage{
      color: var(--Light-Typography-Color-Body-Text, #4B465C);
      font-feature-settings: 'clig' off, 'liga' off;

      /* Light/Basic Typography/Paragraph Semi Bold */
      font-family: "Public Sans";
      font-size: 15px;
      font-style: normal;
      font-weight: 600;
      line-height: 22px; /* 146.667% */
    }
    .house-adress{
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
      overflow: hidden;
      color: var(--Light-Typography-Color-Heading-Text, #4B465C);
      font-feature-settings: 'clig' off, 'liga' off;

      /* Light/Basic Typography/Paragraph Small */
      font-family: "Public Sans";
      font-size: 13px;
      font-style: normal;
      font-weight: 400;
      line-height: 20px; /* 153.846% */
    }

    .link-source{
      display: flex;
      align-items: center;
      gap: 5px;
      align-self: stretch;
      color: var(--Light-Typography-Color-Muted-Text, #4B465C);
      font-feature-settings: 'clig' off, 'liga' off;

      /* Light/Basic Typography/Caption */
      font-family: "Public Sans";
      font-size: 11px;
      font-style: normal;
      font-weight: 400;
      line-height: 14px; /* 127.273% */
      opacity: 0.5;
    }
  }

  .sale-type{
    color: var(--Light-Solid-Color-Primary-Primary---900, #7367F0);
    font-feature-settings: 'clig' off, 'liga' off;

    /* Light/Basic Typography/Paragraph Small */
    font-family: "Public Sans";
    font-size: 13px;
    font-style: normal;
    font-weight: 400;
    line-height: 20px; /* 153.846% */
  }

  .item-salary{
    color: var(--Light-Solid-Color-Primary-Primary---900, #7367F0);
    font-feature-settings: 'clig' off, 'liga' off;

    /* Light/Basic Typography/Paragraph Small Bold */
    font-family: "Public Sans";
    font-size: 13px;
    font-style: normal;
    font-weight: 700;
    line-height: 20px; /* 153.846% */
  }

  .item-fullName{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    gap: 4px;
    .author-name{
      color: var(--Light-Typography-Color-Body-Text, #4B465C);
      font-feature-settings: 'clig' off, 'liga' off;

      /* Light/Basic Typography/Paragraph Small */
      font-family: "Public Sans";
      font-size: 13px;
      font-style: normal;
      font-weight: 400;
      line-height: 20px; /* 153.846% */
    }
    .total-post{
      display: flex;
      padding: 2px 4px;
      flex-direction: column;
      justify-content: center;
      align-items: flex-start;
      gap: 10px;
      background: var(--dark-opacity-color-gray-gray-8, rgba(134, 146, 208, 0.08));
      color: var(--light-solid-color-primary-primary-500-base, #7367F0);
      font-feature-settings: 'clig' off, 'liga' off;

      /* Light/Basic Typography/Paragraph Small */
      font-family: "Public Sans";
      font-size: 13px;
      font-style: normal;
      font-weight: 400;
      line-height: 20px; /* 153.846% */
    }
  }

  .item-action {
    display: flex;
    gap: 16px;
    align-items: center;

    .accept-btn {
      display: flex;
      width: 32px;
      height: 32px;
      justify-content: center;
      align-items: center;
      gap: 10px;
      flex-shrink: 0;
      border-radius: 6px;
      background: var(--light-opacity-color-success-success-8, rgba(40, 199, 111, 0.08));
    }

    .delete-btn {
      display: flex;
      width: 32px;
      height: 32px;
      justify-content: center;
      align-items: center;
      gap: 10px;
      flex-shrink: 0;
      border-radius: 6px;
      background: var(--light-opacity-color-danger-danger-8, rgba(234, 84, 85, 0.08));
    }
  }
}
</style>
