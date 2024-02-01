<script setup>
import avatar1 from '@images/avatars/avatar-1.png'
</script>

<template>
  <div class="header-right-user-section cursor-pointer">
    <VBadge
      dot
      location="bottom right"
      offset-x="3"
      offset-y="3"
      bordered
      color="success"
      class="cursor-pointer"
    >
      <VAvatar
        color="primary"
        variant="tonal"
      >
        <VImg :src="avatar1"/>
      </VAvatar>
    </VBadge>

    <span class="font-black">Vũ Minh Anh Tuấn</span>

    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none">
      <path d="M6 9L12 15L18 9" stroke="#4B465C" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
      <path d="M6 9L12 15L18 9" stroke="white" stroke-opacity="0.2" stroke-width="1.5" stroke-linecap="round"
            stroke-linejoin="round"/>
    </svg>

    <!-- SECTION Menu -->
    <VMenu
      activator="parent"
      width="230"
      location="bottom end"
      offset="14px"
    >
      <VList>
        <!-- 👉 User Avatar & Name -->
        <VListItem>
          <template #prepend>
            <VListItemAction start>
              <VBadge
                dot
                location="bottom right"
                offset-x="3"
                offset-y="3"
                color="success"
              >
                <VAvatar
                  color="primary"
                  variant="tonal"
                >
                  <VImg :src="avatar1"/>
                </VAvatar>
              </VBadge>
            </VListItemAction>
          </template>

          <VListItemTitle class="font-weight-semibold">
            John Doe
          </VListItemTitle>
          <VListItemSubtitle>Admin</VListItemSubtitle>
        </VListItem>

        <VDivider class="my-2"/>

        <!-- 👉 Profile -->
        <VListItem link>
          <template #prepend>
            <VIcon
              class="me-2"
              icon="tabler-user"
              size="22"
            />
          </template>

          <VListItemTitle>Profile</VListItemTitle>
        </VListItem>

        <!-- 👉 Settings -->
        <VListItem link>
          <template #prepend>
            <VIcon
              class="me-2"
              icon="tabler-settings"
              size="22"
            />
          </template>

          <VListItemTitle>Settings</VListItemTitle>
        </VListItem>

        <!-- 👉 Pricing -->
        <VListItem link>
          <template #prepend>
            <VIcon
              class="me-2"
              icon="tabler-currency-dollar"
              size="22"
            />
          </template>

          <VListItemTitle>Pricing</VListItemTitle>
        </VListItem>

        <!-- 👉 FAQ -->
        <VListItem link>
          <template #prepend>
            <VIcon
              class="me-2"
              icon="tabler-help"
              size="22"
            />
          </template>

          <VListItemTitle>FAQ</VListItemTitle>
        </VListItem>

        <!-- Divider -->
        <VDivider class="my-2"/>

        <!-- 👉 Logout -->
        <VListItem to="/login">
          <template #prepend>
            <VIcon
              class="me-2"
              icon="tabler-logout"
              size="22"
            />
          </template>

          <VListItemTitle>Logout</VListItemTitle>
        </VListItem>
      </VList>
    </VMenu>
    <!-- !SECTION -->
  </div>
</template>

<style lang="scss" scoped>
.header-right-user-section {
  display: flex;
  gap: 16px;
  align-items: center;

  .font-black {
    color: #000;
    text-align: center;
    font-feature-settings: 'clig' off, 'liga' off;

    /* Light/Basic Typography/Paragraph Semi Bold */
    font-family: "Public Sans";
    font-size: 15px;
    font-style: normal;
    font-weight: 600;
    line-height: 22px; /* 146.667% */
  }
}
</style>
