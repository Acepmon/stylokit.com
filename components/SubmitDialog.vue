<template>
  <HeadlessTransitionRoot appear :show="isOpen ? true : false" as="template">
    <HeadlessDialog as="div" @close="closeModal" class="relative z-10">
      <HeadlessTransitionChild
        as="template"
        enter="duration-300 ease-out"
        enter-from="opacity-0"
        enter-to="opacity-100"
        leave="duration-200 ease-in"
        leave-from="opacity-100"
        leave-to="opacity-0"
      >
        <div class="fixed inset-0 bg-backdrop" />
      </HeadlessTransitionChild>

      <div class="fixed inset-0 overflow-y-auto">
        <div
          class="flex min-h-full items-center justify-center p-4 text-center"
        >
          <HeadlessTransitionChild
            as="template"
            enter="duration-300 ease-out"
            enter-from="opacity-0 scale-95"
            enter-to="opacity-100 scale-100"
            leave="duration-200 ease-in"
            leave-from="opacity-100 scale-100"
            leave-to="opacity-0 scale-95"
          >
            <HeadlessDialogPanel
              class="relative w-full max-w-80 transform overflow-hidden rounded-lg bg-hover p-8 text-left align-middle shadow-xl transition-all"
            >
              <IconButton @click="closeModal" variant="secondary" class="absolute top-4 right-4">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-[20px]">
                  <path fill-rule="evenodd" d="M5.47 5.47a.75.75 0 0 1 1.06 0L12 10.94l5.47-5.47a.75.75 0 1 1 1.06 1.06L13.06 12l5.47 5.47a.75.75 0 1 1-1.06 1.06L12 13.06l-5.47 5.47a.75.75 0 0 1-1.06-1.06L10.94 12 5.47 6.53a.75.75 0 0 1 0-1.06Z" clip-rule="evenodd" />
                </svg>
              </IconButton>
              <HeadlessDialogTitle
                as="h3"
                class="heading-4 text-primary"
              >
                Submit a website
              </HeadlessDialogTitle>
              <div class="mt-2">
                <p class="body-2 text-help">
                  Found a site you fancy? If it clicks with us too, watch for it in our catalog!
                </p>
              </div>

              <SubmitForm class="mt-6" @submit="submit" :loading="submitFormLoading" :success="submitFormSuccess" />
            </HeadlessDialogPanel>
          </HeadlessTransitionChild>
        </div>
      </div>
    </HeadlessDialog>
  </HeadlessTransitionRoot>
</template>

<script setup lang="ts">
const isOpen = defineModel();
const submitFormLoading = ref(false);
const submitFormSuccess = ref(false);

function submit() {
  submitFormLoading.value = true;
  setTimeout(() => {
    submitFormLoading.value = false;
    submitFormSuccess.value = true;
  }, 2000);
}

function closeModal() {
  isOpen.value = false;
}
</script>