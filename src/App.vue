<template>
  <div>
    <section>
      <header class="bg-[#FFE942]">
        <div class="px-4 mx-auto sm:px-6 lg:px-8 xl:px-12">
          <div class="flex items-center justify-between h-16 lg:h-[72px]">
            <div class="flex items-center flex-shrink-0">
              <a href="#" title="" class="inline-flex">
                <span class="sr-only">Bitcoin Whitepaper</span>
              </a>
            </div>

            <div class="hidden lg:flex lg:justify-center lg:ml-16 lg:space-x-8 xl:space-x-14">
              <a
                href="#"
                title=""
                class="text-base font-medium text-gray-900 transition-all duration-200 rounded focus:outline-none hover:text-gray-700 focus:ring-2 focus:ring-offset-2 focus:ring-gray-900"
              >
                About Bitcoin
              </a>
              <a
                href="#"
                title=""
                class="text-base font-medium text-gray-900 transition-all duration-200 rounded focus:outline-none hover:text-gray-700 focus:ring-2 focus:ring-offset-2 focus:ring-gray-900"
              >
                Resources
              </a>
              <a
                href="#"
                title=""
                class="text-base font-medium text-gray-900 transition-all duration-200 rounded focus:outline-none hover:text-gray-700 focus:ring-2 focus:ring-offset-2 focus:ring-gray-900"
              >
                Community
              </a>
            </div>
          </div>
        </div>
      </header>

      <div class="relative py-12 bg-[#FFE942] overflow-hidden sm:py-16 lg:py-20">
        <div class="relative px-4 mx-auto sm:px-6 lg:px-8 max-w-7xl">
          <div class="max-w-6xl mx-auto">
            <div class="grid items-center grid-cols-1 gap-y-12 lg:grid-cols-2 gap-x-16 xl:gap-x-24">
              <div class="max-w-lg mx-auto text-center lg:max-w-none lg:mx-0 lg:order-2 lg:text-left">
                <p class="text-base font-medium text-gray-600">
                  Découvrez les bases de la finance décentralisée
                </p>
                <h1 class="mt-5 text-3xl font-bold text-gray-900 lg:mt-8 sm:text-4xl xl:text-5xl xl:leading-tight">
                  Obtenez le livre blanc Bitcoin de Satoshi Nakamoto
                </h1>

                <div class="mt-10 lg:mt-14">
                  <p class="text-base font-bold text-gray-900">
                    Entrez votre e-mail pour recevoir le livre blanc après paiement
                  </p>

                  <form @submit.prevent="sendWhitepaper">
                    <div>
                      <input
                        v-model="email"
                        type="email"
                        name="email"
                        id="email"
                        placeholder="Votre adresse e-mail"
                        required
                        class="block w-full px-4 py-3 text-base font-normal leading-7 text-gray-900 placeholder-gray-500 bg-white border border-white rounded-md focus:ring-gray-900 focus:border-gray-900"
                      />
                    </div>

                    <div class="mt-3">
                      <button
                        type="submit"
                        :disabled="isSubmitting"
                        class="inline-flex w-full lg:w-auto items-center justify-center px-6 py-3 text-base font-bold leading-7 text-white transition-all duration-200 bg-gray-900 border border-transparent rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-900 hover:bg-gray-600 focus:ring-offset-[#FFE942] disabled:opacity-50"
                      >
                        {{ isSubmitting ? 'Envoi en cours...' : 'Payer et recevoir le livre blanc' }}
                      </button>
                    </div>

                    <p
                      v-if="message"
                      class="mt-4 text-sm"
                      :class="{
                        'text-green-600': messageType === 'success',
                        'text-red-600': messageType === 'error',
                      }"
                    >
                      {{ message }}
                    </p>
                  </form>
                </div>
              </div>

              <div class="relative lg:order-1">


                <div class="relative">
                  <img
                    class="w-full max-w-xs mx-auto xl:max-w-sm"
                    src="https://images-na.ssl-images-amazon.com/images/S/compressed.photo.goodreads.com/books/1681306228i/117300731.jpg"
                    alt="Bitcoin Whitepaper"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import axiosInstance from './api/axios'; 

const email = ref('');
const isSubmitting = ref(false);
const message = ref('');
const messageType = ref('');

const sendWhitepaper = async () => {
  if (!email.value) {
    message.value = 'Veuillez entrer une adresse e-mail valide.';
    messageType.value = 'error';
    return;
  }

  isSubmitting.value = true;
  message.value = '';
  messageType.value = '';

  try {

    const response = await axiosInstance.post('/payment', {
      email: email.value,
      amountSats: 1,
      description: 'Paiement pour le livre blanc Bitcoin',
    });

    if (response.data.success && response.data.payment?.checkoutLink) {
      window.open(response.data.payment.checkoutLink, '_blank');
      message.value = 'Paiement initié !';
      messageType.value = 'success';
      email.value = '';
    } else {
      throw new Error('Lien de paiement non disponible.');
    }
  } catch (error) {
    console.error('Erreur lors de l\'initiation du paiement :', error);
    message.value = 'Échec de l\'initiation du paiement. Veuillez réessayer.';
    messageType.value = 'error';
  } finally {
    isSubmitting.value = false;
  }
};
</script>

<style scoped>

</style>